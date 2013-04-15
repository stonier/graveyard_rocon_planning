Design of Capabilities
======================

Capabilities are intended to be a higher level interface on top of ROS constructs like topics, services, and dynamic parameters, which are setup and tuned on a per robot basis by the robot developer. These capabilities are a common interface which can be used by both robot developers and robotic app developers to agree upon the ROS interface for a given "capability" required by the application and provided by the robot.

Conceptual Overview
===================

The conceptual overview of capabilities and their related topics should be covered before detailing the design and implementation of Capabilities.

Terminology
-----------

Robot Developers
^^^^^^^^^^^^^^^^

`Robot Developers`_ are the developers who are responsible for setting up software for a particular model or configuration of a robot. Many pieces of software which need to be wrapped up and provided in a consistent way require robot specific tuning. This could be anything like addresses of hardware, robot models, or robot specific parameters a navigation stack. The `Robot Developers`_ is responsible for tuning and organizing these software stacks into discrete "capabilities" which can be advertised to any robot agnostic applications.

App Developers
^^^^^^^^^^^^^^

`App Developers`_ are the developers of robotics related applications. These developers differ from `Robot Developers`_ in that they write applications which are robot agnostic. The apps can depend on "capabilities" provided by robots to perform some task.

Robot Apps (rapps)
^^^^^^^^^^^^^^^^^^

`Robot Applications`_ or rapps_ are applications which are robot agnostic, but in this context are distinctly different from Android Applications. **??** should there be a distinction, or should a rapp be any app (or software) which utilizes the capabilities in a robot agnostic fashion?

Capabilities
^^^^^^^^^^^^

Capabilities_ are interfaces consisting of many elements which are used by both robot developers and robotic app developers. Capabilities_ consist of these elements:

- **name**: Name of the Capability Interface, e.g. *RGBCamera*, *Navigation*, or *MobileBase*
- **topics**: ROS topics, described by their *name*, *type*, and whether or not the topic is expected to be inbound or outbound.
- **services**: ROS services, described by their *name* and *type*.
- **actions**: ROS actionlib actions, described by their *name* and *type*.
- **dynamic_parameters**: ROS dynamic parameters, described by their *name* and *type*.
- **requires**: list of other Capabilities_ which this Capability_ requires. **??** should capabilities be able to depend on other capabilities?

Capabilities_ consist only of the interface declaration, and they do not implement the interface but instead serve as a common reference for both the app developer and the robot developer.

.. image:: images/general_interface_provider_relation.png
