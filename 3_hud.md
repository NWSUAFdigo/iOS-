#  HUD

## 1 概念
- HUD：又被称为`指示器`、`蒙版`、`遮盖`
- 作用：HUD经常用作在完成某个事件后向用户提示某种信息，如：下载完成、网络中断等
- 表现形式：弹出HUD，然后过一段时间消失

## 2 `一段时间后再执行某段代码`的常用方法
- 方法1 
    ```objc
    - (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay;
    // 在delay秒后执行调用该方法对象中的某个方法
    
    // 例：在1.5秒后执行self对象中的test方法，该方法无参数
    [self performSelector:@selector(test) withObject:nil afterDelay:1.5f]
    ```
- 方法2：GCD
    ```objc
    dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(1.5 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
            self.hud.alpha = 0.0f;
        });
    // 在1.5秒后执行代码块中的代码，此时的代码为self.hud.alpha = 0.0f;
    ```
- 方法3：NSTimer
    ```objc
    + (NSTimer *)scheduledTimerWithTimeInterval:(NSTimeInterval)ti target:(id)aTarget selector:(SEL)aSelector userInfo:(nullable id)userInfo repeats:(BOOL)yesOrNo;
    // 在ti秒后调用aTarget对象的某个方法，并选择是否每隔ti秒重复调用该方法
    
    // 例：1.5秒后调用self的test方法，不重复
    [NSTimer scheduledTimerWithTimeInterval:1.5 target:self selector:@selector(test) userInfo:nil repeats:NO];
    ```