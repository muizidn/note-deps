require 'xcodeproj'

platform :ios, 9.0
use_frameworks!

$workspace = 'Deps.xcworkspace'

workspace $workspace
pod 'SwiftGRPC'

post_install do |installer|
  installer.pods_project.recreate_user_schemes
  installer.pods_project.targets.each do |target|
    Xcodeproj::XCScheme.share_scheme(installer.pods_project.path, target.name)
  end
  installer.pods_project.save()
  # Exit here otherwise user scheme will be generated
  # and shared schemes will not be recognized by Carthage
  exit(0)
end

Dir.mkdir $workspace unless Dir.exists?($workspace)
File.open($workspace + '/contents.xcworkspacedata', 'w') do |f|
  f.write <<~STR
  <?xml version="1.0" encoding="UTF-8"?>
  <Workspace
    version = "1.0">
    <FileRef
        location = "group:Pods/Pods.xcodeproj">
    </FileRef>
  </Workspace>
STR
end