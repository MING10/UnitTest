# UnitTest
iOS UnitTest 简要说明

iOS单元测试UnitTest
command+u快捷方式运行 command+6跳转所有UntiTest

1.XCTestCase 生命周期 类方法只调用一次
+

(void)setUp{
[super setUp];
}
############
期间循环
- (void)setUp {
[super setUp];
}
- (void)testExample {
// This is an example of a functional test case.
}
- (void)tearDown {
// Put teardown code here. This method is called after the invocation of each test method in the class.
[super tearDown];
}
##############
+

(void)tearDown{
[super tearDown];
}

2.demo
1）测试的三段式基本结构
- (void)testAdd{
//1. Given 测试条件的准备。
int a = 1;
int b = 1;
//2.When 调用需要测试的方法。
int c = [self addNumberOne:a andNumberTwo:b];
//3.Then 断言判断是否符合预期结果。
XCTAssertEqual(c, 2);
}
- (int)addNumberOne:(int)numberA andNumberTwo:(int)numberB {
return numberA +

numberB;
}
2)测试性能例子
- (void)testPerformanceExample {
// This is an example of a performance test case.
[self measureBlock:^{
// Put the code you want to measure the time of here.
// 需要测试性能的代码
}];
}
3）异步断言测试
- (void)testSendRequestAsync {
//1.创建一个测试断言 Given
XCTestExpectation * expectation = [self expectationWithDescription:@"Async Test was failed"];
//2. When
[self.vc sendRequestAsync:^(id responseObj) {
//Then
XCTAssertNotNil(responseObj);
[expectation fulfill]; // 指定时间内没有执行这个方法，异常对象就会抛出。
}];
// 指定异步测试需要的时间。
[self waitForExpectationsWithTimeout:3 handler:^(NSError * _Nullable error) {
NSLog(@"%@", error);
}];
}
3.常用各种断言
XCTFail(format…) 生成一个失败的测试；
XCTAssertNil(a1, format...)为空判断，a1为空时通过，反之不通过；
XCTAssertNotNil(a1, format…)不为空判断，a1不为空时通过，反之不通过；
XCTAssert(expression, format...)当expression求值为TRUE时通过；
XCTAssertTrue(expression, format...)当expression求值为TRUE时通过；
XCTAssertFalse(expression, format...)当expression求值为False时通过；
XCTAssertEqualObjects(a1, a2, format...)判断相等，[a1 isEqual:a2]值为TRUE时通过，其中一个不为空时，不通过；
XCTAssertNotEqualObjects(a1, a2, format...)判断不等，[a1 isEqual:a2]值为False时通过；
XCTAssertEqual(a1, a2, format...)判断相等（当a1和a2是 C语言标量、结构体或联合体时使用, 判断的是变量的地址，如果地址相同则返回TRUE，否则返回NO）；
XCTAssertNotEqual(a1, a2, format...)判断不等（当a1和a2是 C语言标量、结构体或联合体时使用）；
XCTAssertEqualWithAccuracy(a1, a2, accuracy, format...)判断相等，（double或float类型）提供一个误差范围，当在误差范围（+/-accuracy）以内相等时通过测试；
XCTAssertNotEqualWithAccuracy(a1, a2, accuracy, format...) 判断不等，（double或float类型）提供一个误差范围，当在误差范围以内不等时通过测试；
XCTAssertThrows(expression, format...)异常测试，当expression发生异常时通过；反之不通过；（很变态） XCTAssertThrowsSpecific(expression, specificException, format...) 异常测试，当expression发生specificException异常时通过；反之发生其他异常或不发生异常均不通过；
XCTAssertThrowsSpecificNamed(expression, specificException, exception_name, format...)异常测试，当expression发生具体异常、具体异常名称的异常时通过测试，反之不通过；
XCTAssertNoThrow(expression, format…)异常测试，当expression没有发生异常时通过测试；
XCTAssertNoThrowSpecific(expression, specificException, format...)异常测试，当expression没有发生具体异常、具体异常名称的异常时通过测试，反之不通过；
XCTAssertNoThrowSpecificNamed(expression, specificException, exception_name, format...)异常测试，当expression没有发生具体异常、具体异常名称的异常时通过测试，反之不通过

参考：https://www.cnblogs.com/QianChia/p/6379191.html

4.OCMock 单元测试 创造所需条件测试
下载：https://github.com/erikdoe/ocmock
http://ocmock.org/reference/





