# 用于记录PX4学习的笔记
## 一. Ubuntu, PX4, Gazebo的安装
Ubuntu(一个操作系统): CSDN随便看\
PX4(飞控程序)+Gazebo(一个仿真环境): https://www.guyuehome.com/8983
## 二. 地面站
地面站在PC上获取飞控信息以及给PC发送指令等(通过数传或WIFI或数据线(?))
常用地面站软件有有两种: QGroundControl(QGC)和MissionPlanner(MP)\
PX4官方文档使用的QGC所以我们暂时使用QGC作为地面站. (不过好像MP功能更强大)\
*不过我们不打算使用地面站对飞机进行过多的控制, 考虑到可能会做视觉, 而且负责飞控部分的人是两位计科人, 所以打算采用MAVSDK-python对飞控进行控制*



---
# 问题记录
- [ ] 2022.7.4前: MAVSDK控制固定翼时, 出现了一次起飞降落一次后模式改变拒绝起飞的问题. 
    - 通过重启飞控解决, 但显然有更好的通过切换模式解决的方法. 
       **TODO**: 寻找mavsdk切换模式的方法
- [ ] 2022.7.4前: MAVSDK控制固定翼mission时, 因为mavsdk.mission中没有降落任务, mission upload被PX4拒绝, 原因是PX4之前的某次更新中新增了对固定翼mission的限制: 必须要有landing. 
    - 解决方法1: 在浏览github时注意到了一些mavsdk的插件, 这个问题好像很早就被发现, 有专门的插件做mission_fixed_wing\
    https://github.com/iwishiwasaneagle/MAVSDK-Proto/tree/mission_fixed_wing \
        **TODO**: 研究一下怎么使用
    - 解决方法2: 二次开发飞控, 浏览过论坛和github后, 得知是参数RTL_TYPE在某次更新变为了1(对固定翼来说更安全的返航方式), 网传改成0就好了(?)
    - 解决方法3: 使用旧版飞控, 但是也不知道是那个版本...
