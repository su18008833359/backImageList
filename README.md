/*class RootViewController : UIViewController {
- (void)loadView {
NSLog(@"!!!!!!!!!!!!!!!!!!!!!!!!!!!!mango dispatch_sync");
}
}
*/

declare struct MyStruct {
    typeEncoding:"{MyStruct=dd}",
    keys:x,y
}

class ViewController:UIViewController {

- (void)sequentialStatementExample{
//变量定义
    NSString *text = @"1";
    self.resultView.text = text;

}





- (void)ifStatementExample{
	int a = 2;
	int b = 2;

	NSString *text;
	if(a > b){
		text = @"执行结果: a > b";
	}else if (a == b){
		text = @"执行结果: a == b";
	}else{
		text = @"执行结果: a < b";
	}
	self.resultView.text = text;
}

- (void)switchStatementExample{
	int a = 2;
	NSString *text;
	switch(a){
		case 1:{
			text = @"match 1";
			break;
		}
		case 2:{} //case 后面的一对花括号不可以省略
		case 3:{
			text = @"match 2 or 3";
			break;
		}
		case 4:{
			text = @"match 4";
			break;
		}
		default:{
			text = @"match default";
		}
	}
	self.resultView.text = text;
}

- (void)forStatementExample{
	NSString *text = @"";
	for(int i = 0; i < 20; i++){
		text = text + i + @", ";
		if(i == 10){
			break;
		}
	}
	self.resultView.text = text;
}

- (void)forEachStatementExample{
	NSArray *arr = @[@"a", @"b", @"c", @"d", @"e", @"f", @"g", @"g", @"i", @"j",@"k"];
	NSString *text = @"";
	for(id element in arr){
		text = text + element + @", ";
		if(element.isEqualToString:(@"i")){
			break;
		}

	}
	self.resultView.text = text;
}

- (void)whileStatementExample{
	int a;
	while(a < 10){
		if(a == 5){
			break;
		}
		a++;
	}
	self.resultView.text = @""+a;
}

- (void)doWhileStatementExample{
	int a = 0;
	do{
		a++;
	}while(NO);
	self.resultView.text = @""+a;

}

- (void)blockStatementExample{
	Block catStringBlock = ^NSString *(NSString *str1, NSString *str2){
								NSString *result = str1.stringByAppendingString:(str2);
								return result;
							};
	NSString *result = catStringBlock(@"hello ", @"world!");
	self.resultView.text = result;
}


- (void)paramPassingExampleWithBOOLArg:(BOOL)BOOLArg intArg:(int) intArg uintArg:(NSUInteger)uintArg blockArg:(Block)blockArg  objArg:(id)objArg {
	NSString *text = @"";
	text += @"BOOLArg:" + BOOLArg + @",\n";
	text += @"intArg:" + intArg + @",\n";
    text += @"uintArg:" + uintArg + @",\n";
	text += @"Block执行结果:" + blockArg(@"hello", @"mango") + @"\n";
	text += @"objArg:" + objArg;
	self.resultView.text = text;
}


- (struct MyStruct)paramPassingExampleWithStrut:(struct CGRect)rect{
    struct MyStruct myStruct = {x:(rect.origin.x + 100), y:(rect.origin.x + 10)};
    return myStruct;
}

- (Block)returnBlockExample{
	NSString *prefix = @"mango: ";
	Block catStringBlock = ^NSString *(NSString *str1, NSString *str2){
		NSString *result = str1.stringByAppendingString:(str2);
		return prefix + result;
	};
	return catStringBlock;
}


- (void)callOriginalImp{
    self.ORGcallOriginalImp();
}

- (void)createAndOpenNewViewControllerExample{
	SubMyController *vc = SubMyController.alloc().init();
	self.navigationController.pushViewController:animated:(vc,YES);

}

//类方法替换示例
+ (void)classMethodExapleWithInstance:(ViewController *)vc{
	vc.resultView.text = @"here is Mango  Class Method " + self;
}

//条件注释示例
#If($systemVersion.doubleValue() > 12.0 )
- (void)conditionsAnnotationExample{
self.resultView.text = @"here is Mango method";
}


//GCD示例
- (void)gcdExample{
	dispatch_queue_t queue = dispatch_queue_create("com.plliang19.mango", DISPATCH_QUEUE_CONCURRENT);
	dispatch_async(queue, ^{
		NSLog(@"mango dispatch_async");
	});
	dispatch_sync(queue, ^{
		NSLog(@"mango dispatch_sync");
	});
}


}

int a = 1;

class SuperMyController:UIViewController{

- (void)viewDidLoad {
    super.viewDidLoad();
    self.view.backgroundColor = UIColor.blueColor();
    self.testMasonry();
}


- (void)testMasonry{
    UIView *superview = self.view;
    UIView *view1 = UIView.alloc().init();
    view1.translatesAutoresizingMaskIntoConstraints = NO;
    view1.backgroundColor = UIColor.greenColor();
    superview.addSubview:(view1);
    struct UIEdgeInsets padding = UIEdgeInsetsMake(10, 10, 10, 10);
    view1.mas_makeConstraints:(^(MASConstraintMaker *make) {
        make.top.equalTo()(superview.mas_top).with.offset()(padding.top); //with is an optional semantic filler
        make.left.equalTo()(superview.mas_left).with.offset()(padding.left);
        make.bottom.equalTo()(superview.mas_bottom).with.offset()(-padding.bottom);
        make.right.equalTo()(superview.mas_right).with.offset()(-padding.right);
    });
}





}


class SubMyController:SuperMyController {
@property (strong, nonatomic) UIView *rotateView;
- (void)viewDidLoad {
        super.viewDidLoad();
		self.title = @"Magno 创建自定义ViewController";
		double width = 100;
		double height = 100;
		double x = self.view.frame.size.width/2 - width/2;
		double y = self.view.frame.size.height/2 - height/2;
		UIView *view = CustomView.alloc().initWithFrame:(CGRectMake(x, y, width, height));
		self.view.addSubview:(view);
		view.backgroundColor = UIColor.redColor();
		self.rotateView = view;


        __weak id weakSelf = self;
        self.block = ^{
            __strong id strongSelf = weakSelf;
            NSLog(strongSelf.class());
        };
}

}
