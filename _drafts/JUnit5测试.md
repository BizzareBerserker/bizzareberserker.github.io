---
layout: post
title: "JUnit5测试"
tag: junit springboot
category: essay
---

### JUnit5框架

![JUnit5](/assets/springboot_2.png)

- **JUnit Platform**: 在JVM上启动测试框架的基础，支持多个测试引擎
- **JUnit Jupiter**: JUnit5的核心，包含了一个可在JUnit Platform上运行的测试引擎
- **JUnit Vintage**: 提供了兼容JUnit4.x, JUnit3.x的旧测试引擎

### 测试注解

|注解|描述|
|---|---|
|`@Test`|表明方法是一个测试方法|
|`@ParameterizedTest`|表明方法是一个参数化测试方法，测试方法会从指定的ValueSource获取函数参数并重复执行该方法|
|`@RepeatedTest(value)`|表明方法是一个重复测试方法，该方法会执行value次|
|`@Nested`|标注一个嵌套测试类|

|注解|描述|
|---|---|
|`@BeforeEach`|该方法会在每一个测试方法前执行|
|`@AfterEach`|该方法会在每一个测试方法后执行|
|`@BeforeAll`|该方法会在所有测试前执行一次|
|`@AfterAll`|该方法会在所有测试后执行一次|
|`@DisplayName`|表明方法的测试名|
|`@Tag`|给测试方法分组，类似于`@Category`|
|`@Disable`|禁用该测试方法 (该测试方法会被跳过)|
|`@Timeout`|如果该方法的执行时间超出指定时间单位，则会抛出异常|
|`@ExtendWith`|类似于`@RunWith`|

用于参数化测试: 
|注解|描述|
|---|---|
|`@ValueSource`|设定参数源为指定的数组 (从该数组中依次取值执行测试)|
|`@NullSource`|设定参数源为Null (用null填充参数)|
|`@EnumSource`|设定参数源为指定的枚举|
|`@CsvFileSource`|从指定的CSV文件中获取参数|
|`@MethodSource`|从指定的函数的返回值中获取参数 (返回值应为一个包含参数序列的Stream)|

### 测试方法

- 断言方法: 如果参数不满足断言条件，测试失败

|方法|
|---|
|`assertEquals`|
|`assertNotEquals`|
|`assertSame`|
|`assertNotSame`|
|`assertTrue`|
|`assertFalse`|
|`assertNull`|
|`assertNotNull`|
|`assertArrayEquals`|
|`assertAll`|
|`assertThrows`|
|`assertTimeout`|
|`fail`|

- 前置条件: 如果参数值不满足前置条件，则测试会被跳过

|方法|
|---|
|`assumeTrue`|
|`assumeFalse`|
|...|