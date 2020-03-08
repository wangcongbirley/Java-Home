@Aspect:标识当前类为一个切面容器

@Before:前置增强方法

@Pointcut("execution(表达式)"):

                      1.表达式除了exexution外，还有within/this/target等

@Configuration：该类作为xml配置文件中的<beans>，配置了Spring容器。

@Bean:方法级别的注解，添加Bean的id为方法名。

                       1.生命周期回调：@Bean(initMethod="init")

                       2.自定义Bean的命名:@Bean(name="myFoo")

                       3.添加Bean的描述：@Description('')

@EnableMBeanExport(*.class):避免Spring重复注入bean

@Conditional(*.class):代码中设置条件装载不同的bean

@Api @ApiOperation @ApiImplicitParam :swaggerUI注解

@PreAuthorize("")：一个方法是否能被调用

@DeleteMapping("")：对应删除，是一个删除URL映射

@PutMapping()

@Document(indexName="",type="")

@Filed(index=,analyzer="",searchAnalyzer="",store=true,type=)

@Entity

@Table

@Column(nullable=false,length=40)

@JoinTable

 

@Modifying：和@Query一起使用：自定义更新操作

@Query()

@Scheduled(cron="")：启动服务时执行定时任务

cron表达式：代表触发时间，字符串以5到6个空格隔开

使用数字和特殊字符：* ？ - ， 等

//看到Security包了，mark！

@Component：不属于各种归类(控制器/服务类/数据库类等)，又想交给Spring容器管理，使用此注解。
