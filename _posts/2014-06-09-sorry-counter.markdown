---
layout: post
title:  "Sorry Counter"
category: apps
excerpt: "App allows you to count your sorries."
---

![App Icon][icon]

App allows you to count your sorries. 

Features:

 - Count sorries; 
 - View total amount of sorries.

Implementation
--------------

Actions:

{% highlight obj-c %}
- (void)setCounterText
{
    NSInteger count = [SCModel sharedInstance].count;
    self.counterLabel.text = [[NSNumber numberWithLong:count] stringValue];
}

- (IBAction)sorryButtonAction:(id)sender
{
    [SCModel sharedInstance].count += 1;
    [self setCounterText];
}
{% endhighlight %}

Data model:

{% highlight obj-c %}
NSString* const COUNT_KEY = @"count";

@implementation SCModel

- (id)init
{
    self = [super init];
    if (self) {
        _count = 0;
    }
    return self;
}

+ (SCModel*)sharedInstance
{
    static SCModel* _sharedInstance = nil;
    static dispatch_once_t oncePredicate;
    dispatch_once(&oncePredicate, ^{ _sharedInstance = [self new]; });
    return _sharedInstance;
}

- (void)saveData
{
    NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
    [defaults setInteger:self.count forKey:COUNT_KEY];
    [defaults synchronize];
}

- (void)loadData
{
    NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
    self.count = [defaults integerForKey:COUNT_KEY];
}

@end
{% endhighlight %}

[icon]: /assets/img/sorry-counter/icon.png
