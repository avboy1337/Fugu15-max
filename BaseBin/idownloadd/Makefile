XCODE_PROJECT = src/idownloadd.xcodeproj
XCODE_SCHEME = idownloadd
CS_FLAGS = CODE_SIGN_IDENTITY="" CODE_SIGNING_REQUIRED=NO CODE_SIGNING_ALLOWED=NO
CONFIGURATION = Release

OUTPUT_NAME = idownloadd

build:
	xcodebuild -archivePath ./.build -project $(XCODE_PROJECT) -scheme $(XCODE_SCHEME) -configuration $(CONFIGURATION) -destination generic/platform=iOS archive $(CS_FLAGS)
	@cp -f ./.build.xcarchive/Products/usr/local/bin/$(OUTPUT_NAME) .
	@rm -rf ./.build.xcarchive
	@install_name_tool -change "/var/jb/basebin/libjailbreak.dylib" "@loader_path/libjailbreak.dylib" $(OUTPUT_NAME)
	@ldid -Sentitlements.plist $(OUTPUT_NAME)

clean:
	xcodebuild -project $(XCODE_PROJECT) -scheme $(XCODE_SCHEME) -configuration $(CONFIGURATION) -destination generic/platform=iOS clean
	@rm $(OUTPUT_NAME)

default: build