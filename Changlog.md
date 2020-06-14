# Changelog 0.0.2 发布时间：2020/6/14

## 1. 新增功能

1. 游戏界面的绘制：包括显示地图，退出按钮，阳光数量(初始200)，当前生命值
2. 塔的创建：左键点击草格即可创建塔，同时阳光值-100
3. 敌人：生成，血条显示，在地图中移动，如果最终没有死亡则攻击
4. 塔的攻击：攻击范围是周围一圈的敌人，一秒钟一次，单击25，敌人生命值100
5. 死亡判断，生命值<=0则game over

## 2. 修改功能：无

## 3. 需要实现的基础功能：

1. 敌人、塔的升级
2. 不同种类的塔，敌人，敌人随机生成
3. 删除塔
4. 游戏难度的增加
5. 音乐、美工
6. 对文件架构的优化

## 4. 具体到文件、类、函数

### 一个头文件对应了一个自定义类，因此后面不再重复说明

#### class mainwindow://主窗口

MainWindow(QWidget *parent = nullptr);//绘制主窗口的控件，布局
void paintEvent(QPaintEvent *);//主窗口背景

#### class game://游戏界面

explicit Game(QWidget *parent = nullptr);//绘制游戏界面

void settower(QPoint & p);//在指定位置生成塔
void setteki();//生成敌人
void attack();//塔攻击敌人
void deleleteki();//死亡敌人的清除
void paintEvent(QPaintEvent *) Q_DECL_OVERRIDE;//绘制塔、敌人、地图
void mousePressEvent(QMouseEvent *event) Q_DECL_OVERRIDE;//生成塔
void timerEvent(QTimerEvent *event) Q_DECL_OVERRIDE;//用于攻击、生成敌人、死亡判断等需要定时器的事件
void die();//判断是否死亡

#### class teki://敌人

teki(QPoint pos,QString fileloc);//构造函数
void draw(QPainter * painter);//绘图，血条
void move();//在地图中移动
QPoint getpos();//获取当前位置

#### class Tower://塔

Tower(QPoint pos,QString fileloc);//构造函数
void draw(QPainter * painter);//绘图
QPoint getpos();//获取位置

#### class gameover://game over界面

explicit gameover(QWidget *parent = nullptr);//绘制窗口

#### head.h: 对于头文件的集中管理