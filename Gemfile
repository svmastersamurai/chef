source "https://rubygems.org"
gemspec name: "chef"

gem "activesupport", "< 4.0.0", group: :compat_testing, platform: "ruby"

gem "chef-config", path: "chef-config" if File.exist?(__FILE__ + "../chef-config")

# Ensure that we can always install rake, regardless of gem groups
gem "rake"

gem "ffi", github: "lamont-granquist/ffi", branch: "lcg/rb_gc_guard_ptr" if RUBY_PLATFORM.downcase =~ /aix/

group(:docgen) do
  gem "yard"
end

group(:maintenance) do
  gem "tomlrb"

  # To sync maintainers with github
  gem "octokit"
  gem "netrc"
end

group(:pry) do
  gem "pry"
  gem "pry-byebug"
  gem "pry-stack_explorer"
end

group(:ruby_prof) do
  # may need to disable this in insolation on fussy builds like AIX, RHEL4, etc
  gem "ruby-prof"
end

group(:development, :test) do
  gem "simplecov"
  gem "rack", "~> 1.5.1"

  # for testing new chefstyle rules
  # gem 'chefstyle', github: 'chef/chefstyle'
  gem "chefstyle", git: "https://github.com/chef/chefstyle.git", branch: "master"

  gem "ruby-shadow", platforms: :ruby unless RUBY_PLATFORM.downcase =~ /(aix|cygwin)/
end

group(:travis) do
  # See `bundler-audit` in .travis.yml
  gem "bundler-audit", git: "https://github.com/rubysec/bundler-audit.git", ref: "4e32fca"
end

instance_eval(ENV["GEMFILE_MOD"]) if ENV["GEMFILE_MOD"]

# If you want to load debugging tools into the bundle exec sandbox,
# add these additional dependencies into chef/Gemfile.local
eval(IO.read(__FILE__ + ".local"), binding) if File.exist?(__FILE__ + ".local")
