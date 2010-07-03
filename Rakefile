require 'open-uri'

YCPATH = ENV['YCPATH'] ||
         ENV['HOME'] + '/local/package/yui/yuicompressor-latest.jar'

SRC = ['init',
       'timeline',
       'band',
       'themes',
       'ethers',
       'ether-painters',
       'event-utils',
       'labellers',
       'sources',
       'original-painter',
       'detailed-painter',
       'overview-painter',
       'compact-painter',
       'decorators',
       'units',
       'l10n/en/timeline',
       'l10n/en/labellers'].map { |x| "scripts/#{x}.js" }

CSS = ['timeline',
       'ethers',
       'events'].map { |x| "styles/#{x}.css" }

task :default => :package

desc "Build package"
task :package => ['timeline-bundle.js', 'timeline-bundle.css']

file 'timeline-bundle.js' => SRC do |t|
  concat(t.prerequisites, t.name)
  yui_compressor(t.name)
end

file 'timeline-bundle.css' => CSS do |t|
  concat(t.prerequisites, t.name)
  yui_compressor(t.name)
end

def yui_compressor(filename)
  sh "java -jar #{YCPATH} -o #{filename} #{filename}"
  puts "Compressed #{filename}"
end

def concat(srclist, outfile)
  open(outfile, 'w') do |f|
    srclist.each do |src|
      f.write(open(src).read)
      puts "Wrote #{src} to #{outfile}"
    end
  end
end