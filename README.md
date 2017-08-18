## Repository to run the multi map navigation package for SDP 2016 course

### Setting up
* dependencies:
    * ```ros-indigo-move-base```
    * ```amcl (from mdr_2dnav)```
* launch steps:
    * ```roscore```
    * ```roslaunch mdr_bringup(_sim) robot.launch```
    * start mongodb: ```sudo mongod --dbpath=/path/to/database```
    * add new maps (name main map ```BRS 069``` to work with default launch file)
        * GUI:
            * ```roslaunch multi_map_navigation map_settings.launch```
            * ```rosrun rviz rviz -d map_settings.rviz```
             (```map_settings.rviz``` under ```.../multi_map_navigation/rviz/```)
        * terminal?
   * launch move base node: ```roslaunch multi_map_navigation move_base_sdp.launch```

### Maps management:
* rename maps: ```rosservice call /rename_map "map_id: '87721635-3eed-4361-8d7b-52697165b690' new_name: 'BRS 069'"```
* list maps: ```rosservice call /list_maps "{}"```

### Update maps names

* terminal: mongo
* db.adminCommand({listDatabases :1})
* use map_store
* Query db.map.find()
* Problem: all maps are named new map:
* Update : db.maps.update({name: "New Map"}, {$set: {name: "<new_name>"}})
