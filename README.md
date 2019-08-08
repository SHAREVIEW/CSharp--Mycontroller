# CSharp--Mycontroller
C# Windows应用窗体用户自定义控件--开关实现
利用两个开关图片实现开关控件





沿袭之前的做法，本人还是喜欢直接PS好图片后，用drawimage方法将图片绘制到用户控件上，启用双缓冲和背景透明，有些人说PS一张精美的图片也不是很容易，需要专业的，这里提供一个好方法，让你也可以获取到这些图片，其实大部分的APP都可以用解压软件打开，拓展名改为.zip即可，解压出来一般里面都含有绝大部分的图片，发现绝大部分的APP都喜欢用图片作为背景来展示一些效果，而不是原原本本的用代码一点点绘制。腾讯就是腾讯啊，大公司！人家的美工MM设计的图片那真的没得话说，绝对一流，手机QQ每次升级一个版本，都会下过来将里面的精美图片图标之类的提取出来，以便项目使用，（这不会算是盗版吧！）好了，开始正文吧！

第一步：先准备开关按钮要使用到的背景图片，一般就两张，一张是开的，一张是关的，也可以说是开启和关闭，如下图：

  

然后将这些图片都作为资源文件添加到项目中。

 

第二步：新建用户控件

在构造函数中设置双缓冲和背景透明以及控件大小。 

this.SetStyle(ControlStyles.AllPaintingInWmPaint, true);
 
           this.SetStyle(ControlStyles.DoubleBuffer, true);
 
           this.SetStyle(ControlStyles.ResizeRedraw, true);
 
           this.SetStyle(ControlStyles.Selectable, true);
 
           this.SetStyle(ControlStyles.SupportsTransparentBackColor, true);
 
           this.SetStyle(ControlStyles.UserPaint, true);
 
           this.BackColor = Color.Transparent;
 
 
 
           this.Cursor = Cursors.Hand;
 
           this.Size = new Size(87, 27);
第三步：定义一个公共属性，这样的话外部就可以访问当前选中状态，这里也命名为Checked

 

bool isCheck = false;
 
  
 
        /// <summary>
 
        /// 是否选中
 
        /// </summary>
 
        public bool Checked
 
        {
 
            set { isCheck = value; this.Invalidate(); }
 
            get { return isCheck; }
 
        }
 

 

第四步：根据当前是否选中条件分别绘制图片，在onPaint事件中

这里为了增加多种开关样式，还增加了CheckStyleX属性。

 

protected override void OnPaint(PaintEventArgs e)
 
        {            
 
            Bitmap bitMapOn = null;
 
            Bitmap bitMapOff = null;
 
  
 
            if (checkStyle == CheckStyle.style1)
 
            {
 
                bitMapOn = global::myAlarmSystem.Properties.Resources.btncheckon1;
 
                bitMapOff = global::myAlarmSystem.Properties.Resources.btncheckoff1;                
 
            }
 
            else if (checkStyle == CheckStyle.style2)
 
            {
 
                bitMapOn = global::myAlarmSystem.Properties.Resources.btncheckon2;
 
                bitMapOff = global::myAlarmSystem.Properties.Resources.btncheckoff2;                
 
            }
 
            else if (checkStyle == CheckStyle.style3)
 
            {
 
                bitMapOn = global::myAlarmSystem.Properties.Resources.btncheckon3;
 
                bitMapOff = global::myAlarmSystem.Properties.Resources.btncheckoff3;                
 
            }
 
            else if (checkStyle == CheckStyle.style4)
 
            {
 
                bitMapOn = global::myAlarmSystem.Properties.Resources.btncheckon4;
 
                bitMapOff = global::myAlarmSystem.Properties.Resources.btncheckoff4;                
 
            }
 
            else if (checkStyle == CheckStyle.style5)
 
            {
 
                bitMapOn = global::myAlarmSystem.Properties.Resources.btncheckon5;
 
                bitMapOff = global::myAlarmSystem.Properties.Resources.btncheckoff5;                
 
            }
 
            else if (checkStyle == CheckStyle.style6)
 
            {
 
                bitMapOn = global::myAlarmSystem.Properties.Resources.btncheckon6;
 
                bitMapOff = global::myAlarmSystem.Properties.Resources.btncheckoff6;
 
            }
 
             
 
            Graphics g = e.Graphics;
 
            Rectangle rec = new Rectangle(0, 0, this.Size.Width, this.Size.Height);
 
  
 
            if (isCheck)
 
            {
 
                g.DrawImage(bitMapOn, rec);
 
            }
 
            else
 
            {
 
                g.DrawImage(bitMapOff, rec);
 
            }
 
        }
 

 到此是不是完成了呢，其实不是，因为鼠标在控件上面单击的时候，还需要改变当前的背景图片，所以必须在Click事件中写

private void myButtonCheck_Click(object sender, EventArgs e)
 
        {
 
            isCheck = !isCheck;
 
            this.Invalidate();
 
        }
