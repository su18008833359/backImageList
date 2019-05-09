class RootViewController : UIViewController {

- (void)loadView {
    // Set EAGLView as view of RootViewController
    //self.view = (__bridge CCEAGLView *)cocos2d::Application::getInstance()->getView();
      self.view.backgroundColor = [UIColor redColor];
}

}
