## LaneKit

LaneKit is an iOS Objective-C code generator for integration with RestKit. It generates
models, resource providers, and full iOS apps with mimimal effort. There is support for unit testing with SenTestingKit
including fixtures and tests. LaneKit is a command line app written in Ruby and packaged as a Ruby Gem.

- [Source code for LaneKit](https://github.com/LarryAasen/LaneKit/zipball/master) from [GitHub](http://github.com).
- Questions? [Stack Overflow](http://stackoverflow.com/questions/tagged/lanekit) is the best place to find answers.

## Benefits
* properly implemented models and resource providers
* easy integration with RestKit
* consistent Objective-C code
* unit tests
* test fixtures in JSON and Objective-C
* iOS app creation fully integrated with CocoaPods and RestKit
* tested code
* rapid development
* enhanced productivity of junior developers
* reduces dependency on senior developers

## How To Get Started

1. Install the LaneKit Ruby Gem from RubyGems.org

        $ gem install lanekit
        Successfully installed lanekit-x.x.x
 
2. LaneKit is ready to use

## Example Usage

### Add a new model called Video to an existing Xcode project.

    $ lanekit generate model Video duration:string headline:string id:integer image:string location:string

      create  Classes/Models
      create  Classes/Tests/Fixtures
      create  Classes/Tests/Models
      create  Classes/Models/Video.h
      create  Classes/Models/Video.m
      create  Classes/Tests/Fixtures/VideoFixtures.h
      create  Classes/Tests/Fixtures/VideoFixtures.m
      create  Classes/Tests/Fixtures/VideoFixtures.one.json
      create  Classes/Tests/Fixtures/VideoFixtures.two.json
      create  Classes/Tests/Models/VideoTest.h
      create  Classes/Tests/Models/VideoTest.m
      create  Classes/Models/LKModel.h
      create  Classes/Models/LKModel.m

and here is the Objective-C header file that was generated by LaneKit:

```objective-c
//
//  Video.h
//
//  This model was created on 2013-10-20 by LaneKit v0.3.0.
//
// The following LaneKit command was used to generate this file:
// lanekit generate model Video duration:string headline:string id:integer image:string location:string
//

#import "LKModel.h"

@interface Video : LKModel

@property (nonatomic,strong) NSString *duration;
@property (nonatomic,strong) NSString *headline;
@property (nonatomic,strong) NSNumber *id;
@property (nonatomic,strong) NSString *image;
@property (nonatomic,strong) NSString *location;

@end
```

and here is the Objective-C .m file that was generated by LaneKit:

```objective-c
//
//  Video.m
//
//  This model was created on 2013-10-20 by LaneKit v0.3.0.
//
// The following LaneKit command was used to generate this file:
// lanekit generate model Video duration:string headline:string id:integer image:string location:string
//

#import "Video.h"

@implementation Video

// Dictionary to convert self to JSON
+ (NSDictionary *)dictionaryForRequestMappings
{
    return @{
             // source key path : destination attribute name
             @"duration": @"duration",
             @"headline": @"headline",
             @"id": @"id",
             @"image": @"image",
             @"location": @"location"
    };
}

// Dictionary to convert JSON to self
+ (NSDictionary *)dictionaryForResponseMappings
{
  return @{
           // source key path : destination attribute name
             @"duration": @"duration",
             @"headline": @"headline",
             @"id": @"id",
             @"image": @"image",
             @"location": @"location"
    };
}

+ (NSString *)keyPath
{
  return @"video";
}

@end
```

and here is the unit test fixtures file that was generated by LaneKit:

```objective-c
//
//  VideoFixtures.m
//
//  This model fixture was created on 2013-08-11 by LaneKit v0.2.0.
//

#import "VideoFixtures.h"

@implementation VideoFixtures

+ (Video *)one
{
  Video *video = Video.new;

  video.duration = @"MyString";
  video.headline = @"MyString";
  video.id = [NSNumber numberWithInteger:1];
  video.image = @"MyString";
  video.itemDate = NSDate.new;
  video.location = @"MyString";

  return video;
}

+ (Video *)two
{
  Video *video = Video.new;

  video.duration = @"MyString";
  video.headline = @"MyString";
  video.id = [NSNumber numberWithInteger:1];
  video.image = @"MyString";
  video.itemDate = NSDate.new;
  video.location = @"MyString";

  return video;
}

@end
```

and here is the RestKit compatible JSON fixture file that was generated by LaneKit:

```json
{
  "video": {
    "duration": "MyString",
    "headline": "MyString",
    "id": "1",
    "image": "MyString",
    "itemDate": "03/01/2012",
    "location": "MyString"
  }
}
```

and here is a unit test that was generated in Models/VideoTest.m by LaneKit:

```objective-c
- (void)testVideoNewOne
{
  Video *video = VideoFixtures.one;
  STAssertNotNil(video, @"video is nil");

  STAssertTrue([video.duration isEqualToString:@"MyString"], @"duration not correct value");
  STAssertTrue([video.headline isEqualToString:@"MyString"], @"headline not correct value");
  STAssertTrue(video.id.integerValue == [NSNumber numberWithInteger:1].integerValue, @"id not [NSNumber numberWithInteger:1]");
  STAssertTrue([video.image isEqualToString:@"MyString"], @"image not correct value");
  STAssertNotNil(video.itemDate, @"itemDate is nil");
}
```

### Add a new model called Contents that contains a list of Videos and uses a relationship mapping.

    $ lanekit generate model contents contents:array:Video
     exist  Classes/model
    create  Classes/model/Contents.h
    create  Classes/model/Contents.m

### Add a new resource provider called Contents.

    $ lanekit generate provider Contents Contents http://scores.espn.go.com/allsports/scorecenter/v2/videos/build?sport=top
    create  Classes/Controllers
    create  Classes/Controllers/LKResourceProvider.h
    create  Classes/Controllers/LKResourceProvider.m
    create  Classes/Controllers/ContentsProvider.h
    create  Classes/Controllers/ContentsProvider.m
    
### Create a new iOS app fully integrated with CocoaPods and RestKit.

    $ lanekit new SportsFrames

### Sample App
The SportsFrames app is a fully functional sample app using RestKit created to demonstrate the use of LaneKit in a real world app. It
has models and resource providers that are generated from LaneKit.
Download the code from [GitHub](https://github.com/larryaasen/SportsFrames).

## Credits

LaneKit was created by [Larry Aasen](https://github.com/larryaasen).

## Contact

Follow Larry Aasen on Twitter [@LarryAasen](https://twitter.com/LarryAasen).

## License

LaneKit is available under the MIT license. See the LICENSE file for more info.
