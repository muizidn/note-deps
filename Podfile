require 'fileutils'
require 'xcodeproj'

platform :ios, 8.0
use_frameworks!

# project 'Deps.xcodeproj'

# target 'Foo' do
  # pod 'SwiftGRPC'
# end

workspace 'Deps.xcworkspace'
pod 'SwiftGRPC'

post_install do |installer|
  installer.pods_project.recreate_user_schemes
  installer.pods_project.targets.each do |target|
    Xcodeproj::XCScheme.share_scheme(installer.pods_project.path, target.name)
  end
  # Exit here otherwise user scheme will be generated
  # and shared schemes will not be recognized by Carthage
  exit(0)
end