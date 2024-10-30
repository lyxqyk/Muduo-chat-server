# 定义了一个SRC_LIST变量，包含了该目录下所有的源文件
aux_source_directory(. SRC_LIST)
aux_source_directory(./db DB_LIST)
aux_source_directory(./model MODEL_LIST)
aux_source_directory(./redis REDIS_LIST)

# 指定生成可执行文件
add_executable(ChatServer ${SRC_LIST} ${DB_LIST} ${MODEL_LIST} ${REDIS_LIST})
# 指定可执行文件链接时需要依赖的库文件
target_link_libraries(ChatServer muduo_net muduo_base mysqlclient hiredis pthread)


# 链接MySQL库
target_link_libraries(ChatServer ${MYSQL_LIBRARIES})

# 包含MySQL的头文件目录
include_directories(${MYSQL_INCLUDE_DIRS})

set(MYSQL_INCLUDE_DIRS "/usr/include/mysql")
set(MYSQL_LIBRARIES "/usr/lib/x86_64-linux-gnu/libmysqlclient.so")

include_directories(${MYSQL_INCLUDE_DIRS})
target_link_libraries(ChatServer ${MYSQL_LIBRARIES})



