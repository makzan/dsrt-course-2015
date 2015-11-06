# Copied/Inspired from Pro Git 2
# https://github.com/progit/progit2/blob/master/Rakefile

namespace :book do
  desc 'prepare build'
  task :prebuild do
    Dir.mkdir 'output' unless Dir.exists? 'output'
    Dir.mkdir 'output/images' unless Dir.exists? 'output/images'
    Dir.mkdir 'images' unless Dir.exists? 'images'
    Dir.glob("book/*/images/*").each do |image|
      FileUtils.copy(image, "output/images/" + File.basename(image))
      FileUtils.copy(image, "images/" + File.basename(image))
    end

    # Copy anything in public
    Dir.glob("public/*").each do |file|
      FileUtils.copy(file, "output/" + File.basename(file))
    end
  end

  desc 'build basic book formats'
  task :build => :prebuild do
    puts "Converting to HTML..."
    `bundle exec asciidoctor -a source-highlighter=highlightjs -D output dsrt-course-2015.adoc`
    puts " -- HTML output at output/dsrt-course-2015.html"

    puts "Converting to EPub..."
    `bundle exec asciidoctor-epub3 -D output dsrt-course-2015.adoc`
    puts " -- Epub output at output/dsrt-course-2015.epub"

    puts "Converting to Mobi (kf8)..."
    `bundle exec asciidoctor-epub3 -a ebook-format=kf8 -D output dsrt-course-2015.adoc`
    puts " -- Mobi output at output/dsrt-course-2015.mobi"

    puts "Converting to PDF... (this one takes a while)"
    `bundle exec asciidoctor-pdf -D output dsrt-course-2015.adoc 2>/dev/null`
    puts " -- PDF  output at output/dsrt-course-2015.pdf"
  end

  desc 'build each chapter'
  task :build_chapter_html => :prebuild do
    puts "Converting chapters to HTML..."
    `bundle exec asciidoctor -D output index.adoc`
    # `bundle exec asciidoctor -a source-highlighter=highlightjs -a linkcss -D output book/*/*.adoc`
    `mkdir output/01-introduction; bundle exec asciidoctor -a source-highlighter=highlightjs -a linkcss -D output/01-introduction book/01-introduction/index.adoc`
    `mkdir output/02-user-interface-design; bundle exec asciidoctor -a source-highlighter=highlightjs -a linkcss -D output/02-user-interface-design book/02-user-interface-design/index.adoc`
    `mkdir output/03-jquery-mobile; bundle exec asciidoctor -a source-highlighter=highlightjs -a linkcss -D output/03-jquery-mobile book/03-jquery-mobile/index.adoc`
    `mkdir output/04-getting-sensor-value; bundle exec asciidoctor -a source-highlighter=highlightjs -a linkcss -D output/04-getting-sensor-value book/04-getting-sensor-value/index.adoc`
    `mkdir output/05-rain-or-not; bundle exec asciidoctor -a source-highlighter=highlightjs -a linkcss -D output/05-rain-or-not book/05-rain-or-not/index.adoc`
    `mkdir output/06-offline-and-storage; bundle exec asciidoctor -a source-highlighter=highlightjs -a linkcss -D output/06-offline-and-storage book/06-offline-and-storage/index.adoc`
    `mkdir output/0x-react; bundle exec asciidoctor -a source-highlighter=highlightjs -a linkcss -D output/0x-react book/0x-react/index.adoc`
    `mkdir output/0x-desktop-web-app; bundle exec asciidoctor -a source-highlighter=highlightjs -a linkcss -D output/0x-desktop-web-app book/0x-desktop-web-app/index.adoc`
    `mkdir output/0x-web-accessibility; bundle exec asciidoctor -a source-highlighter=highlightjs -a linkcss -D output/0x-web-accessibility book/0x-web-accessibility/index.adoc`
    puts " -- HTML output done in output/"
  end
end

task :default => "book:build"
