# 1 准备工作：
## jdk
## tomcat
## myeclipse10.0
## 数据库--oracle
## 工程文件+context.xml

# 2 导入工程到myeclipse

# 3 context.xml文件拷贝到tomcat安装目录下conf文件夹中，替换原来的context.xml

# 4 修改context.xml文件
## 4.1 Resource.username（数据库登录用户名）
## 4.2 Resource.password（数据登录密码）
## 4.3 Resource.url（JDBC连接数据库实例地址）
## 4.4 Resource.name（数据源名称，与application-db.xml中datasource.value要一致）

# 5 在oracle数据库中建立员工表emp和部门表dept两张表，并在表中添加数据  
# 6 项目主数据源配置（查看web.xml>>application-all.xml>>application-db.xml）
	## 6.1 修改bean.datasource.value与context.xml中Resource.name匹配
## 6.2 修改jsp页面votedQryList.jsp中修改要展示的数据属性名
## 6.3 修改控制器RebateController的方法doChannelInit
`List<Map<String, Object>> olist=rebateService.queryStaff();`
## 6.4 修改接口rebateService，增加queryStaff()
`public List<Map<String, Object>> queryStaff();`
## 6.5 修改实现类rebateServiceImpl，增加方法queryStaff()
>public List<Map<String, Object>> queryStaff(){
>	String sql = "select * from staff a inner join dept b on a.dept = b.deptno ";
>	List<Map<String, Object>> list = new ArrayList<Map<String,Object>>();
>	try {
>		list = jdbcBaseDao.getJdbcTemplate().queryForList(sql.toString());
>	} catch (Exception e) {
>	e.printStackTrace();
>}
>	return list;
>}
## 6.6 根据需要修改queryStaff()方法中sql语法，以获得需要的数据

## 7 在myeclipse中配置tomcat
>  windows>>preference>>将自带的tomcat禁用，然后启用跟自己安装的版本匹配的tomcat，并配置tomcat-home-directory

# 8 右击工程文件>>myeclipse>>add and remove project deployments>>deploy project

# 9 run server

# 10 打开浏览器，输入url：http://localhost:8080/rebate/doInit.do即可看到发布的页面