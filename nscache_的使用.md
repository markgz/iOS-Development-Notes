#NSCache 的使用
1. 在做 iOS 开发中，如果涉及到图片的网络加载和缓存处理。通常大家都会想到用第三方的开源类库。
例如 SDWebImage 和 YYWebImage 等。但是如果只是为了实现一个简单的缓存处理。可以选择使用 CocoaTouch framework 的 NSCache 这个类。这个类提供了几个很方便的方法，可以用来添加缓存和得到缓存文件和清除缓存内容。具体的方法名称和操作 NSMutableDictionary 很相似。
有 objectForKey: 和 setObject: forKey: ，removeObjectForKey: removeAllObjects 等方法。

2. 在使用 NSCache 的时候，可以监听 NSNotificationCenter post 的内存警告通知。在收到这个通知后，及时调用 remove 方法将缓存的文件从内存中移除掉。保证 app 不会因为内存紧张而被系统 kill 掉。 

参考代码示例:

	#import "GZMemoryCacheManager.h"
	
	@interface GZMemoryCacheManager ()
	
	@property (strong, nonatomic) NSCache *memoryCache;
	
	@end
	
	@implementation GZMemoryCacheManager
	
	+ (instancetype)shared
	{
	    static GZMemoryCacheManager *inst;
	    static dispatch_once_t onceToken;
	    dispatch_once(&onceToken, ^{
	        inst = [[GZMemoryCacheManager alloc] init];
	        inst.memoryCache = [[NSCache alloc] init];
	        
	        [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(clearMemoryCache) name:UIApplicationDidReceiveMemoryWarningNotification object:nil];
	    });
	    return inst;
	}
	
	- (void)dealloc
	{
	    [[NSNotificationCenter defaultCenter] removeObserver:self];
	}
	
	#pragma mark - Public Methods
	
	- (id)cachedObjectForKey:(NSString *)key
	{
	    if ([NSString isNilOrEmpty:key]) {
	        return nil;
	    }
	    
	    return [self.memoryCache objectForKey:key];
	}
	
	- (void)storeObject:(id)object forKey:(NSString *)key
	{
	    if (![NSString isNilOrEmpty:key]) {
	        [self.memoryCache setObject:object forKey:key];
	    }
	}
	
	- (void)clearMemoryCache
	{
	    [self.memoryCache removeAllObjects];
	}
	
	@end
    