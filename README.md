# 冒险岛游戏项目需求说明书
一、项目背景
1.项目描述
         网络游戏一直以来受广大青少年朋友的喜爱，此项目可以让很多热爱游戏的学生在程序的天堂中畅游一番，编写属于自己的游戏引擎，此项目基于JavaSE窗口的GUI技术，模拟冒险岛Online游戏的画面及游戏效果，完成属于你自己的睿道冒险旅程！
2.项目运营时间
二、项目意义
       运用Java中GUI技术实现桌面游戏，目的是为让大家在编写游戏的过程中，巩固面向对象的编程思想模式，提高大家Java基础技能，并且编写属于自己的第一个大游戏。
三、项目环境
1、硬件
    内存：4G+
   硬盘 ：5G+
CPU ：Intel core i5+
显卡：独立显卡
2、软件
IDE ：Eclipse
JDK：JDKB+
其他软件：Office、PhotoShop 等
四、项目结构
1、项目名称
Neuedu_MapleStory_v1.0
2、包名
com.neuedu.maplestory.*
-client
-util
-images
-entity
-sounds
-constant
3、类名
      首字母大写，符合驼峰式命名
项目结构图：
 
五、系统详细设计
5.1类体描述
（1）类图
 
5.2功能描述
5.2.1创建窗口
使用双缓冲技术解决图片闪烁问题
	// 双缓冲防闪烁
	private Image bufferImage = null;
	@Override
	public void update(Graphics g) {
		if (bufferImage == null) {
			bufferImage = this.createImage(Constant.GAME_WIDTH, Constant.GAME_HEIGHT);
		}
		Graphics gOff = bufferImage.getGraphics();
		Color c = gOff.getColor();
		gOff.setColor(Color.black);
		gOff.fillRect(0, 0, Constant.GAME_WIDTH, Constant.GAME_HEIGHT);
		gOff.setColor(c);
		paint(gOff);
		g.drawImage(bufferImage, 0, 0, null);
	}
5.2.2 构建接口和抽象类
创建移动的接口：
public interface Moveable {
	/**
	 * 所有物体对象都要动（即使原地不动也要实现该接口）
	 */
	void move();
}
创建画的接口：
public interface Drawable {
	/**
	 * 所有对象物体都要画出来
	 * @param g  画笔
	 */
	void draw(Graphics g);
}
创建所有类的父类：
/**
 * 冒险岛中所有类的父类 
 * @author Administrator
 *
 */
public abstract class MapleStoryObject implements Moveable,Drawable {}
5.3.3创建hero类与hero的移动
利用键盘监听来对人物的移动进行控制	
 
5.3.4根据不同方向，更换对应图片
 
5.3.5完成跳的动作
 
5.3.6添加射击（攻击）动作及图片
 
5.3.7子弹类Arrow
Arrow类继承MapleStoryObject类，拥有其中的各种属性。
 
5.3.8怪物类 Mob
对怪物Mob1赋予各种属性，继承自Mob，mob继承与父类MapleStoryObject。
 
5.3.9怪物类死亡效果
 

5.3.10怪物的各种运动状态
                       
5.3.11道具类
 
5.3.12 吃道具
进行碰撞检测，true表示吃到道具，false表示没有吃到。
 
5.3.13与怪物的碰撞
怪物攻击hero，进行碰撞检测，true时，怪物进行攻击的动作，当false时，怪物变为正常动作状态。
 
5.4项目添加音乐
5.4.1 下载第三方API-javalayer
 
 
补充：项目需求
（1）启动界面
 ![](https://img-blog.csdnimg.cn/20190922143755294.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTQxMDgyMQ==,size_16,color_FFFFFF,t_70)
（2）跳台 绳子 梯子
![](https://img-blog.csdnimg.cn/20190922143833958.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTQxMDgyMQ==,size_16,color_FFFFFF,t_70)
（3）声音
 
（4）自由发挥
增加了hero的生命数显示和hero死亡后的图片
当英雄血量为0时，生命数减1，英雄复活，满血满蓝。当英雄生命数等于0时，英雄血量为0时，英雄死亡，无法再次复活，变为死亡图片。
             ![在这里插入图片描述](https://img-blog.csdnimg.cn/201909221439465.png)
