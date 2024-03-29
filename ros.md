# ROS

## Installation

### ROS Installation

```shell

```

### mavros Installation

Binary Installation

```shell
$ sudo apt-get install ros-kinetic-mavros ros-kinetic-mavros-extras
$ wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh
$ sudo bash ./install_geographiclib_datasets.sh   
```

## ROS Python Style

## ROS C++ Style

### Naming Schemes

+ **CamelCased**: starts with  a capital letter, and has a capital letter for each new word, with no underscores
+ **camelCased**: like CamelCased, but with a low-case first letter
+ **under_scored**: uses only low-case letters, words separated by underscores
+ **ALL_CAPITALS**: All capital letters, with separated by underscores

#### Packages

ROS packages are **under_scored**

#### Topics/Services

ROS topics and service names are **under_scored**

#### Files

The file names should be descriptive 

if a file primarily implements a class, name the file after class

All files are **under_scored**

Source files use **.cpp**

Header files use **.h**

Libraries, being files are **under_scored**

```c++
// 系统自带的头文件
#include <>
// 用户自定义的文件
#include ""
```

#### Classes/Types

Class names are CamelCased

**Name the class after what it is**

**Compound names of over three words are a clue that your design may be a unnecessarily confusing **

```c++
class ExampleClass;
class HoKuURGLaser;
```

#### function/Methods

function and class method names are camelCased and the arguments are under_scored

```c++
int exampleMethod(int example_arg);
```

#### Variables

+ variable names are **under_scored**
+ **Constants** are ALL_CAPITALS

**Member variables** 

variables that are members of a class are **under_scored** with a trailing underscore added

```c++
int example_int_;
```

**Global variables**

global variables are **under_scored** with a leading g_ added

```c++
int g_shutdown;
```

#### Namespaces

Namespace names are **under_scored**

#### License statements

Every source and header file must contain a license and copyright statement at the beginning of the file

## Navigating the Ros FileSystem

### Using rospack

+ find option : return the path to package

### USing roscd

+ change a directory directly to a package

### roscd log

+ take you to the folder where ROS stores log files

### USing rosls

+ ls directly in a package by name rather than by absolute path

## Creating a ROS package

### make up a catkin package

+ package structure:

```markdown
mypackage/
	CMakeLists.txt
	package.xml
	include/
	src/
```

+ package in a catkin workspace

```markdown
workspace_folder/
	src/
		CMakLists.txt
		package_1/
			CMakeLists.txt
			package.xml
			include/
			src/
		package_n/
			CMakeLists.txt
			package.xml
			include/
			src/
```

+ create a catkin package

  + First: change to the source space directory of th catkin workspace

  + Second: use catkin_create_pkg to create a new package which depends on std_msgs, roscpp, rospy

    ```shell
    catkin_create_pkg beginner_tutorials std_msgs rospy roscpp
    example:
    catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
    ```

+ building a catkin workspace and sourcing the setup file

  + build the packages in the catkin workspace

    ```shell
    cd ~/catkin_ws
    catkin_make
    ```

  + add the workspace to your ROS environment 

    ```shell
    . ~/catkin_ws/devel/setup.bash
    ```

+ customizing own package

  + description tag

    update the description tag:

    ```markdown
    <description>The beginner_tutorials package</description>
    ```

  + maintainer tags: it lets other know who to contact about the package

    ```markdown
    <maintainer email="you@yourdomain.tld">Your Name</maintainer>
    ```

  + license tags

    ```markdown
    <license>BSD</license>
    ```

  + dependencies tags

    The dependencies are spilt into `build_depend`,`buildtool_depend`,`exec_depend`,`test_depend`

  + final paxkage.xml

## Building a ROS Package

### Building Packages

As longas all of the system dependencies of your package are installed, we can now build your own package.Use the following command:

```shell
# source /opt/ros/<your ros distro>/setup.bash
```

+ Using cattkin_make

  catkin_make combines the calls to cmake and make

  + in a CMake workflow, build command:

    ```shell
    $ mkdir build
    $ cd build
    $ cmake ..
    $ make # make install (optionally)
    ```

  + in a catkin workspace,build command:

    ```shell
    $ catkin_make
    catkin_make [make_targets] [-DCMAKE]
    ```

+ Building your package

  You should already create a catkin workspace and a new catkin package.

  Then go to the catkin workspace, build the package using catkin_make

  ```shell
  cd ~/catkin_ws
  catkin_make
  ```

  After catkin_make command,there will be three folders in your catkin workspace:

  + build :  is the default location of the build space and is where cmake and make are called to configure and build your packages
  + devel : is the default location of the devel space, which is where your executables and libraries go before you install your package
  + src :

## What is ROS Nodes

### Prerequisites : install a lightweight simulator 

```shell
$ sudo apt-get install ros-<distro>-ros-tutorials  # <sidtro> is your ROS distribution
```

### Graph Concepts

+ Nodes : is an executable that uses ROS to communicate with other nodes
+ Messages : ROS data type used when subsribing or publishing a topic
+ Topics : Nodes can publish messages to a topic as well as subscribe to a topic to receive messages
+ Master : Name service for ROS
+ rosout : ROS equivalent of stdout/stderr
+ roscore : Master + rosout + parameter server

### roscore

roscore is the first thing that should run when using ROS

### Using rosnode

+ **rosode list command** :rosnode displays information about the ROS nodes that are currently running, the rosnode list command lists these active nodes 

+ **rosnode info command** : return information about a special node 

### Using rosrun

rosrun allows you to use the package name to directly run a node within a package

Usage : 

```shell
$ rosrun [package_name] [node_name]
```

We can reassign Names from th command-line, The node list will add a node called  your_name

```shell
$ rosrun [package_name] [node_name] __name:=<your name>
```



## What is ROS topics

### Setup--for this tutorial

+ **roscore**

  Make sure that we have a roscore running

+ **turtlesim**

  ```shell
  $ rosrun turtelsim turtlesim_node
  ```

+ **turtle keyboard teleoperation**

  ```shell
  $ rosrun turtlesim turtle_teleop_key
  ```

### ROS Topic

Two nodes are communicating with each other over a ROS Topic, while one publish a topic, while another subscribe the same topic. Using rqt_graph which shows the nodes and the topics currently running.

#### Using rqt_graph

It will show you a communication of two nodes in a graph

![rqt_graph](/run/user/1000/doc/1790e0ad/rqt_graph_turtle_key.png)

#### Introducing rostopic

The **rostopic tool** allow us to get information about ROS **topics**

We can use the help option to get aviable sub-commands for the rostopic :

```shell
$rostopic -h
	rostopic bw    # display bandwidth used  by topic
	rostopic delay # display delay of the topic from timestamp in header
	rostopic echo  # print messages to srceen
	rostopic hz    # display publishing rate of topic
	rostopic find  # find topics by type
	rostopic info  # print information about active topic
	rostopic list  # list active topics
	rostopic pub   # publish data to topic
	rostopic type  # print topic or field type
```

#### Using rostopic echo

#### Using rostopic list

### ROS Message

Communication on topics happensby sending ROS messages between nodes. 

The publisher and subsriber must send and receive the same type of message. 

We can use **rostopic type command** to see what type should we use.

#### Using rostopic type

+ **rosmsg** : show the details of the message 

## Understanding ROS Services and Parameters

### ROS Services

Services are another way that nodes can communicate with each other



### Using rosservice

### Using rosparam

### Using roslaunch

roslaunch starts nodes as defined in a launch file

Usage :

```shell
$ roslaunch [package] [filename.launch]
```

+ First : go to the package we created and built early

  ```shell
  $ roscd [package_name]
  # if roscd has an error 
  # roscd: No such package/stack 'foobar', 
  # you need to source the environment setup file
  $ cd ~/catkin_ws
  $ source devel/setup.bash
  ```

+ Then : make a launch directory and a launch file

+ End : launch your package

### Using rosed

rosed allows you to directly edit a file within a package by using package name rather than typing the entire path to the package

```shell
$ rosed [package_name] [filename]
```

## Introducing to msg and srv

+ **msg** : msg files are simple text files that describe the fields of a ROS message. They are used to generator source code for messages in different languages. 
+ **srv** :an src file describes a service. Composed of a request and a response.

### Using msg

#### Creating a msg

```shell
```



### Using srv





## ROS Packages structure

+ include/package_name : C++ include headers
+ msg : contain message types
+ src/package_name : source files 
+ srv : contain service types
+ scripts : executable scripts
+ CMakeLists.txt : CMake build file
+ package.xml : Package 
+ CHANGELOG.rst



## Issue

+ when open a new terminal, we need to type the command 

  `source ~/catkin/devel/setup.bash`,

  to step this, we can add this command to the ~/.bashrc , so that we can rospack find our package without type command 