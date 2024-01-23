# Protocol | Interface

Syntax for protocol conformance example just to be more sure about how interface / protocols work in Objective-C.

### Header

```objc
@interface CEventData

extern NSString* const KEY_FOR_MEDIA;
extern NSString* const KEY_FOR_WIDTH;
extern NSString* const KEY_FOR_PLAYBACK;

@property(nonatomic, retain)NSString* mediaT;
@property(nonatomic)NSNumber* width;
@property(nonatomic, retain)NSArray* playbackS;

-(NSMutableDictionary*)toDict;
-(void)fromDict:(NSDictionary *)dict;

@end
```

### Implementation

```objc
@interface CEventData ()
{
    NSString* _mediaT;
    NSNumber* _width;
    NSArray* _playbackS;
}
@end

@implementation CEventData

@synthesize mediaT = _mediaT;
@synthesize width = _width;
@synthesize playbackS = _playbackS;

NSString* const KEY_FOR_MEDIA = @"mediaT";
NSString* const KEY_FOR_WIDTH = @"width";
NSString* const KEY_FOR_PLAYBACK = @"playbackS" ;


-(NSMutableDictionary*)toDict { 
	 NSMutableDictionary* dict = [[NSMutableDictionary alloc] init];

    [dict setValue:self.mediaT forKey:KEY_FOR_MEDIA];
    [dict setValue:self.width forKey:KEY_FOR_WIDTH];
    [dict setValue:self.playbackS forKey:KEY_FOR_PLAYBACK];
}

-(void)fromDict:(NSDictionary *)dict {
	self.mediaT = [dict objectForKey:KEY_FOR_MEDIA];
    self.width = [dict objectForKey:KEY_FOR_WIDTH];
    self.playbackS = [dict objectForKey:KEY_FOR_PLAYBACK];
}

@end
```

```objc
@interface CustomState ()

@property (nonatomic, copy) void (^willEnterStateBlock)(CustomState *, TKTransition *);
@property (nonatomic, copy) void (^didEnterStateBlock)(CustomState *, TKTransition *);

@end
```


[SO source](https://stackoverflow.com/questions/22314991/how-to-print-something-to-the-console-in-xcode)
