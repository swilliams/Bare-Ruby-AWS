# $Id: Rakefile,v 1.19 2010/03/20 11:56:30 ianmacd Exp $
#

require 'rubygems'
#Gem::manage_gems

require 'rake/gempackagetask'

spec = Gem::Specification.new do |s|
  s.platform = Gem::Platform::RUBY
  s.name = 'bare-ruby-aws'
  s.version = '0.1'
  s.author = 'Scott Williams'
  s.email =  'scott@krazyyak.com'
  s.summary = 'Basic Ruby interface to search Amazon Associates Web Services'
  s.description = <<-EOF
  A Fork of the Ruby/AWS library that removes operations other than item-search
  and allows a config file location to be specified.

  Ruby/AWS is a Ruby language library that allows the programmer to retrieve
  information from Amazon via the Product Advertising API. In addition to the
  original amazon.com site, amazon.co.uk, amazon.de, amazon.fr, amazon.ca and
  amazon.co.jp are also supported.
  EOF
  s.homepage = 'http://github.com/swilliams/Bare-Ruby-AWS'
  s.files = FileList[ 'lib/*.rb', 'lib/**/*.rb' ].to_a
  s.require_path = 'lib'
  s.test_files = Dir.glob( 'test/*.rb' )
  s.has_rdoc = true
  s.extra_rdoc_files = %w[ COPYING INSTALL NEWS README ]
  s.required_ruby_version = '>= 1.8.6'
#  s.autorequire = 'amazon/aws/search'
end

Rake::GemPackageTask.new( spec ) do |pkg|
  pkg.need_tar = true
end

task :default => "pkg/#{spec.name}-#{spec.version}.gem" do
  puts 'Generated latest version.'
end

desc 'Produce HTML documentation in ./doc'
task :doc do
  system( *%w[ rdoc -SUx CVS lib ] )

  # In-place edit to change page of main frame to the one with the most
  # relevant documentation.
  #
  $-i = ''
  ARGV[0] = 'doc/index.html'
  ARGF.each_line do |l|
    l.sub!( Regexp.new( 'files/lib/.+?\.html' ),
	    'files/lib/amazon/aws_rb.html' )
    puts l
  end
end

desc 'Remove build and installation files'
task :clean do
  FileUtils.rm_rf %w[ InstalledFiles config.save doc/ pkg/ ]
end
