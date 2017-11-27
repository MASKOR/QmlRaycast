# QmlRaycast
Projects and unprojects rays between 2D and 3D space.
This class encapsulates common math for interacting with a 3D scene over a 2D interface.
Use QmlRaycast to express this interaction declaratively and to keep your Qml code clean.

# Features
* intersect ray with plane
* unproject 2d point to ray in 3d space
* unproject 2d point to 3d point at given distance
* unproject 2d point onto given plane
* project 3d point to 2d
* project 3d point onto plane

# What can't it do

* Raycast rendering
* Raycast against 3d geometry (except for planes)

# Usage

Properties of Raycast can be written and read. Depending on which properties are set, the remaining properties will calculate. Most sensible combinations are supported. Propertybindings work. There are qWarnings() if the combination is invalid.

E.g. Display 2D Textlabel over a Point in the 3D Scene. Setting "viewMatrix", "projectionMatrix" and "worldPosition" will make it possible to read "screenPosition".

Register the class to qml:

    qmlRegisterType<QmlRaycast>("fhac.mascor", 1, 0, "Raycast");

# Example:
    Raycast {
        id: mouseRaycast
        viewMatrix: camera.viewMatrix
        projectionMatrix: camera.projectionMatrix
        viewportSize: Qt.size(scene3d.width, scene3d.height)
        pointOnPlane: camera.viewCenter
        planeNormal: camera.viewVector
        screenPosition: Qt.vector2d(sceneMouseArea.mouseX, sceneMouseArea.mouseY)
    }
    
    My3DObject {
        translation: mouseRaycast.worldPosition
    }
