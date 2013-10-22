drchubo_ikfast
==============

IKfast inverse kinematics solvers for DRCHubo with a plugin wrapper for OpenRAVE. The plugin wrapper means that the IKfast solvers are location-independent provided they are in your OPENRAVE_PLUGINS path.

Build and usage instructions
----------------------------
First, clone this repository:
```
$ cd /your/catkin/workspace/src
$ git clone https://github.com/WPI-ARC/drchubo_ikfast.git
$ rospack profile
```

To build all packages in this repository:
```
(in the surrounding Catkin workspace directory)
$ catkin_make
```

To build a particular package in the repository:
```
(in the surrounding Catkin workspace directory)
$ catkin_make --pkg <package name>
```

To use, you must update your `OPENRAVE_PLUGINS` environment variable:
```
$ roscd drchubo_ikfast/plugins
```
Add the current directory to `OPENRAVE_PLUGINS`:
```
$ export OPENRAVE_PLUGINS=current_directory:$OPENRAVE_PLUGINS
```
(You should probably do this in your `.bashrc` file)

Next, you need to edit the `drchubo_v3.robot.xml` model to use the new IK solvers. The new file should look like this:
```
<?xml version="1.0" encoding="utf-8"?>
<Robot name="drchubo_v3" >
    <KinBody file="drchubo_v3.kinbody.xml" makejoinedlinksadjacent="true">
        <translation>0 0 1.175</translation>
    </KinBody>

    <Manipulator name="leftArm">
        <base>Body_Torso</base>
        <effector>leftPalm</effector>
        <direction>0 1 0</direction>
        <iksolver>drchubo_leftarm_ikfast</iksolver>
    </Manipulator>

    <Manipulator name="rightArm">
        <base>Body_Torso</base>
        <effector>rightPalm</effector>
        <direction>0 1 0</direction>
        <iksolver>drchubo_rightarm_ikfast</iksolver>
    </Manipulator>

    <Manipulator name="leftFoot">
        <base>Body_TSY</base>
        <effector>leftFoot</effector>
        <direction>0 0 -1</direction>
    </Manipulator>

    <Manipulator name="rightFoot">
        <base>Body_TSY</base>
        <effector>rightFoot</effector>
        <direction>0 0 -1</direction>
    </Manipulator>

    <Manipulator name="Head">
        <base>Body_Torso</base>
        <effector>Body_NK2</effector>
        <direction>0 0 1</direction>
    </Manipulator>

</Robot>
```
