SRC_FILES = %w{
  api.c
  dumper.c
  emitter.c
  loader.c
  parser.c
  reader.c
  scanner.c
  writer.c
  yaml_private.h
}
INC_FILES = %w{
  yaml.h
}
EXT_FILES = %w{
  README
  LICENSE
  config.h
}

YAML_VERSION = [0,1,4]

require 'fileutils'

task :update_yaml_src do
  if false
    base = "yaml-#{YAML_VERSION.join(".")}"
    tgzfn = "#{base}.tar.gz"
    url = "http://pyyaml.org/download/libyaml/#{tgzfn}"
    sh "wget #{url.inspect}" unless File.exist?(tgzfn)
    sh "tar xzf #{tgzfn}" unless File.directory?(base)
    sh "cd #{base.inspect}; ./configure"
    FileUtils.mkdir_p("src")
    (
      SRC_FILES.map { |f| "#{base}/src/#{f}" } +
      INC_FILES.map { |f| "#{base}/include/#{f}" } +
      EXT_FILES.map { |f| "#{base}/#{f}" }
    ).each { |fn|
      puts "copying #{fn}"
      FileUtils.cp fn, "src/#{File.basename(fn)}"
    }
    FileUtils.rm_rf(base)
  end
end

task :update_version do
  sh "/usr/libexec/PlistBuddy -c 'Set :CFBundleShortVersionString \"#{YAML_VERSION.join(".")}\"' Yaml/Yaml-Info.plist"
end

task :default => [:update_yaml_src, :update_version] do
end