Heroku buildpack for Ruby
======================

云帮 Java 语言 Maven 项目的源码构建核心部分是基于[Heroku buildpack for java](http://devcenter.heroku.com/articles/buildpack) 来实现的。

## 工作原理

当buildpack检测您代码的根目录下有 Gemfile 文件时，您的应用会被识别为Ruby应用。针对不同的ruby web开发框架有如下识别方式：

- 源码根目录存在 [config.ru](http://config.ru/) 文件，会被识别为 Rack 应用。
- 源码跟目录存在 config/environment.rb 文件，会被识别为Rails 2 应用。
- 源码根目录存在 config/application.rb文件且文件中包含Rails::Application 字符串，会被识别为Rails 3/Rails 4 应用。

buildpack使用`Bundler 1.7.12`来进行项目的依赖管理，用户无法指定版本。

## 文档

以下文档了解更多：

- [云帮支持Ruby](http://www.rainbond.com/docs/stable/user-lang-docs/ruby/lang-ruby-overview.html#part-2ed464e4df97e11f)

- [Rails应用描述](http://www.rainbond.com/docs/stable/user-lang-docs/ruby/rails-framework/lang-ruby-rails-overview.html)

- [部署Rails3.x应用](http://www.rainbond.com/docs/stable/user-lang-docs/ruby/rails-framework/lang-ruby-rails3.x-deploy.html)

- [使用Puma部署Rails应用](http://www.rainbond.com/docs/stable/user-lang-docs/ruby/rails-framework/lang-ruby-rails-puma.html)

## 配置

### 环境变量

以下环境将被自动设置：

```bash
GEM_PATH => vendor/bundle/#{RUBY_ENGINE}/#{RUBY_ABI_VERSION}
LANG => en-us
PATH => bin:vendor/bundle/#{RUBY_ENGINE}/#{RUBY_ABI_VERSION}/bin:/usr/local/bin:/usr/bin:/bin
```

>  `GEM_PATH` 设置`/vendor`目录主要用来帮助`bundler`管理`gem`

### 指定一个Ruby版本

云帮默认版本为`Ruby 2.0.0`，您也可以通过Gemfile来指定一个版本：

```ruby
source "https://ruby.taobao.org" 
ruby "1.9.3"
```

> 提示：由于国外的gem源速度比较慢，推荐使用淘宝的gem源

如需指定非 MRI 的 ruby 引擎，需要使用 `:engine` 和 `:engine_version` 。您可以通过以下内容指定 JRuby ：

```bash
ruby "1.9.3", :engine ="jruby", :engine_version ="1.7.8"
```

也可以通过在程序中执行以下 Ruby 代码指定版本

```bash
ruby ENV['CUSTOM_RUBY_VERSION'] || '2.0.0'
```

## 授权

根据 MIT 授权证获得许可。 请参阅LICENSE文件
