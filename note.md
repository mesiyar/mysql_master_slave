docker mysql主从配置
1. master 配置
    server_id 在同一局域网内需要保持唯一性
    binlog-ignore-db=mysql  指定不需要同步的库
    binlog-do-db=xxx       指定需要同步的库
2. slave 配置 
    read_only=1    只读设置

3. master 上操作
    创建用户  create user xxx@xxx identity by xxx
    授权      grant REPLICATION slave, REPLICATION  client on *.* to xxx@xxx
    查看主从同步状态  show master status; 主要为了获取 logbin file 和 position

4. slave 操作
    指定 master   change master to master_host=  , master_user= , master_password= , master_port=, master_log_file=. master_log_pos, master_connect_retry = 
    开启主从 start slave 
    若 出现 slave 启动失败  可以 reset slave 再次start
    执行 show slave status  主要看 slave_io_running 和 slave_sql_running 两个值是否为 yes
    