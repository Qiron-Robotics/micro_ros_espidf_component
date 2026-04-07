cmake_minimum_required(VERSION 3.8)
project(interfaces_package)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

find_package(rosidl_default_generators REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}  

  # Messages
  "msg/DefaultReturn.msg"
  "msg/Pose.msg"

  # 1 Publisher  - Feedback 
  # 1 Subscriber - Goal 
  # 3 Services   - Execução
  "action/PlayMovement.action" 
  
  # 6 Services 
  "srv/MovementsSendCommand.srv"
  "srv/MovementsGetPose.srv"
  "srv/MovementsSetPose.srv"
  "srv/MovementsPing.srv"
  "srv/MovementsReadAddress.srv"
  "srv/MovementsWriteAddress.srv"

  # 1 Publisher 
  "msg/BluetoothMessage.msg" 

  # 3 Services 
  "srv/BluetoothGetStatus.srv"
  "srv/BluetoothSendCommand.srv"
  "srv/BluetoothSendMessage.srv"

  # 1 Publisher 
  "msg/SystemWarning.msg"

  # 1 Service 
  "srv/SystemSendCommand.srv"

  # Total de topicos ROS:
  #   - Services:    13
  #   - Publishers:   3   
  #   - Subscriber:   1 

  )

ament_package()