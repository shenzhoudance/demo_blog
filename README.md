# Let's Build: With Ruby On Rails - Blog With Comments

## 案例分析：

### 构建 demo_blog 的案例的关键在于完成三个维度的动作：

- （1） gem 安装和调试；
- （2） 增删改查 的功能；
- （3） 评论功能 的调试；
- （4） 样式功能 的修改；

# demo_blog 的最终效果
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsle85n6oj31kw0twtbo.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsldzv9xmj31kw0omdif.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsldrv83oj31kw0rdq57.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsldmrzi9j31kw0tf417.jpg)

```
cd workspace
rails new demo_blog
ls
cd demo_blog
ls
git init
git status
git add .
git commit -m "initial commit"
rails server
git remote add origin https://github.com/shenzhoudance/demo_blog.git
git push -u origin master
```
![image](https://ws4.sinaimg.cn/large/006tNc79gy1fpre75f7c0j317w0me0yi.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpre47c21ej31040y0az2.jpg)

```
git checkout -b gem
https://rubygems.org/
gem 'better_errors', '~> 2.4'
gem 'bulma-rails', '~> 0.6.2'
gem 'simple_form', '~> 3.5', '>= 3.5.1'
---
group :development do
---
gem 'guard', '~> 2.14', '>= 2.14.2'
gem 'guard-livereload', '~> 2.5', '>= 2.5.2'
---
bundle install
git add .
git commit -m "add gems"
```
https://bulma.io/documentation/overview/start/
https://github.com/guard/guard-livereload
http://livereload.com/extensions/
```
rails generate simple_form:install
gem 'guard-livereload', '~> 2.5', '>= 2.5.2', require: false
bundle
rails s
bundle exec guard
exit
```
![image](https://ws2.sinaimg.cn/large/006tNc79ly1fpsbhgsktij313207wmza.jpg)
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsbfs8wjmj31kw0p87d6.jpg)
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsbgpxuv6j31hw0rq45t.jpg)
```
git status
git add .
git commit -m "add gems"
git push origin gem
```
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsbjx835fj31b80vgjyp.jpg)

# Github 上传方法

![image](https://ws3.sinaimg.cn/large/006tNc79ly1fpsbmo5v3bj31kw0rx0zk.jpg)
![image](https://ws3.sinaimg.cn/large/006tNc79ly1fpsbmjwlqgj31800qydjc.jpg)
![image](https://ws3.sinaimg.cn/large/006tNc79ly1fpsbmfh6rxj31960sgjx2.jpg)
![image](https://ws2.sinaimg.cn/large/006tNc79ly1fpsbm8x3bvj318w0sktee.jpg)
```
rails g controller --help
```
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsbu2iq0rj314k10sagy.jpg)

```
git checkout -b posts
---
rails g controller posts

rails g model Post title:string content:text
rake db:migrate

recources :posts
root 'posts#index'

index.html.erb
show.html.erb
new.html.erb
edit.html.erb
_form.html.erb

---
app/assets/stylesheets/application.scss
@import "bulma";
```
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsd0phf70j30v009qaar.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsd17beltj30ic07674n.jpg)

```
app/controllers/posts_controller.rb
---
class PostsController < ApplicationController
   def index
     @posts = Post.all.order("created_at DESC")
  end

  def new
    @post = Post.new
  end

  def create
    @post = Post.new(post_params)

    if @post.save
      redirect_to @post
    else
      render 'new'
    end
  end

  def show
    @post = Post.find(params[:id])
end

 def update
   @post = Post.find(params[:id])

   if @post.update(post_params)
     redirect_to @post
   else
     render 'edit'
   end
 end

 def edit
  @post = Post.find(params[:id])
 end

 def destroy
   @post = Post.find(params[:id])
   @post.destroy
   redirect_to root_path
 end

  private

  def post_params
    params.require(:post).permit(:title, :content)
 end
end
---
app/views/posts/_form.html.erb
---
<%= simple_form_for @post do |f| %>
<%=f.input :title %>
<%=f.input :content %>
<%=f.button :submit %>
<% end %>
---
app/views/posts/new.html.erb
---
<h1>New Post</h1>
<%= render 'form' %>

---
app/views/posts/show.html.erb
---
<h1><%= @post.title %></h1>
<p><%= @post.content %></p>

<%= link_to "Home", root_path, class: "button" %>
<%= link_to "Edit", edit_post_path(@post), class: "button" %>
<%= link_to "Delete", post_path(@post), method: :delete, data: { confirm: "are you sure? " }, class: "button" %>


---
app/views/posts/index.html.erb
---
<% @post.each do |post| %>
<h1><%= link_to post.title, post %></h1>
<p><%= post.content %><p>
<% end %>

<p><%= link_to "New Post", new_post_path %><p>

```
# post 的最终效果
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsipe1f85j30s20acq41.jpg)
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsiorwjcbj30p60ckdgk.jpg)
![image](https://ws4.sinaimg.cn/large/006tNc79ly1fpsip5qecsj30u00aw0tx.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79ly1fpsip0wzz9j30p80by75d.jpg)

```
git status
git add .
git commit -m "add post CRUD"
git push origin posts
```
# comment 评论功能构建
```
git checkout -b comment
rails g controller comments
rails g model Comment name:string comment:text
rake db:migrate


rails g migration AddPostIdToComments
---
db/migrate/20180328064613_add_post_id_to_comments.rb
---
class AddPostIdToComments < ActiveRecord::Migration[5.1]
  def change
    add_column :comments, :post_id, :integer
  end
end
---
rake db:migrate
---
```
```
app/models/comment.rb
---
class Comment < ApplicationRecord
  belongs_to :post
end
---
app/models/post.rb
---
class Post < ApplicationRecord
  has_many :comments
end
---
```
```
config/routes.rb
---
Rails.application.routes.draw do
 resources :posts do
   resources :comments
  end

 root 'posts#index'
end
---

app/controllers/comments_controller.rb
---
class CommentsController < ApplicationController

  def create
    @post = Post.find(params[:post_id])
    @comment = @post.comments.create(params[:comment].permit(:name, :comment))
    redirect_to post_path(@post)

end

def destroy
  @post = Post.find(params[:post_id])
  @comment = @post.comments.find(params[:id])
  @comment.destroy
  redirect_to post_path(@post)
end

end
---
app/views/comments/_from.html.erb
---
<%= simple_form_for([@post, @post.comments.build]) do |f| %>
<%=f.input :name %>
<%=f.input :comment %>
<%=f.button :submit %>
<% end %>
---


app/views/comments/_comment.html.erb
---
<p>
  <%= comment.name %>:
  <%= comment.comment %>
</p>

<%= link_to 'Delete', [comment.post, comment],
               method: :delete, class: "button is-danger", data: { confirm: 'Are you sure?' } %>
---

app/views/posts/show.html.erb
---
<h1><%= @post.title %></h1>
<p><%= @post.content %></p>

<%= link_to "Home", root_path, class: "button" %>
<%= link_to "Edit", edit_post_path(@post), class: "button" %>
<%= link_to "Delete", post_path(@post), method: :delete, data: { confirm: "are you sure? " }, class: "button" %>


<p><%= @post.comments.count %> Comments</p>

<%= render @post.comments %>
<p>leave a reply</p>
<%= render 'comments/from' %>
---
```

# comment 的最终效果
![image](https://ws2.sinaimg.cn/large/006tNc79gy1fpskiobs7lj30ms0a2q3q.jpg)
![image](https://ws2.sinaimg.cn/large/006tNc79gy1fpski68p8ej30oi0nedhm.jpg)

```
rails console
2.3.1 :001 > @post = Post
2.3.1 :002 > @Post.connection
2.3.1 :003 > @post.connection
2.3.1 :004 > @post.all
2.3.1 :005 > @post = Post.find(3)
2.3.1 :006 > @post
2.3.1 :007 > @post.title = "this is a nice to you!"
2.3.1 :008 > @post.save
2.3.1 :009 > exit
---
```
![image](https://ws4.sinaimg.cn/large/006tNc79gy1fpsk9co0rmj31kw0lcaku.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsk97cwqjj31kw0jlgtu.jpg)

```
git status
git add .
git commit -m "add comment to post"
git push origin comment
```
![image](https://ws4.sinaimg.cn/large/006tNc79gy1fpskmt270uj31cs0te467.jpg)

```
git checkout -b layouts-css
---
app/views/layouts/application.html.erb
---
<!DOCTYPE html>
<html>
  <head>
    <title>DemoBlog</title>
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
  	<section class="hero is-primary is-medium">
	  <!-- Hero head: will stick at the top -->
	  <div class="hero-head">
	    <nav class="navbar">
	      <div class="container">
	        <div class="navbar-brand">
	          <%= link_to 'Demo Blog', root_path, class: "navbar-item" %>
	          <span class="navbar-burger burger" data-target="navbarMenuHeroA">
	            <span></span>
	            <span></span>
	            <span></span>
	          </span>
	        </div>
	        <div id="navbarMenuHeroA" class="navbar-menu">
	          <div class="navbar-end">
	            <%= link_to "Create New Post", new_post_path, class:"navbar-item" %>
	          </div>
	        </div>
	      </div>
	    </nav>
	  </div>

	  <!-- Hero content: will be in the middle -->
	  <div class="hero-body">
	    <div class="container has-text-centered">
	      <h1 class="title">
	        <%= yield :page_title %>
	      </h1>
	    </div>
	  </div>
	</section>
    <%= yield %>
  </body>
</html>
---
app/views/posts/_form.html.erb
---
<div class="section">
<%= simple_form_for @post do |f| %>
  <div class="field">
    <div class="control">
      <%= f.input :title, input_html: { class: 'input' }, wrapper: false, label_html: { class: 'label' } %>
    </div>
  </div>

  <div class="field">
    <div class="control">
      <%= f.input :content, input_html: { class: 'textarea' }, wrapper: false, label_html: { class: 'label' }  %>
    </div>
  </div>
  <%= f.button :submit, class: "button is-primary" %>
<% end %>
</div>
---
app/views/posts/edit.html.erb
---
<% content_for :page_title, "Edit Post" %>
<%= render 'form' %>
---
app/views/posts/new.html.erb
---
<% content_for :page_title, "Create a new post" %>
<%= render 'form' %>
---
app/views/posts/show.html.erb
---
<% content_for :page_title, @post.title %>

<section class="section">
	<div class="container">
		<nav class="level">
		  <!-- Left side -->
		  <div class="level-left">
		    <p class="level-item">
		        <strong>Actions</strong>
		    </p>
		  </div>
		  <!-- Right side -->
		  <div class="level-right">
		  	<p class="level-item">
		    	<%= link_to "Edit", edit_post_path(@post), class:"button" %>
		  	</p>
		  	<p class="level-item">
				<%= link_to "Delete", post_path(@post), method: :delete, data: { confirm: "Are you sure?" }, class:"button is-danger" %>
				</p>
		  </div>
		</nav>
		<hr/>

		<div class="content">
			<%= @post.content %>
		</div>
	</div>
</section>


<section class="section comments">
	<div class="container">
		<h2 class="subtitle is-5"><strong><%= @post.comments.count %></strong> Comments</h2>
		<%= render @post.comments %>
		<div class="comment-form">
			<hr />
			<h3 class="subtitle is-3">Leave a reply</h3>
	 		<%= render 'comments/from' %>
		</div>
	</div>
</section>

---
app/views/posts/index.html.erb
---
<% content_for :page_title,  "Index" %>

<div class="section">
	<div class="container">
		<% @posts.each do |post| %>
			<div class="card">
		  <div class="card-content">
		    <div class="media">
		      <div class="media-content">
		        <p class="title is-4"><%= link_to post.title, post  %></p>
		      </div>
		    </div>
		    <div class="content">
		     	<%= post.content %>
		    </div>
		    <div class="comment-count">
		    	<span class="tag is-rounded"><%= post.comments.count %> comments</span>
		    </div>
		  </div>
		</div>
		<% end %>
	</div>
</div>
---

app/views/comments/_comment.html.erb
---
<div class="box">
  <article class="media">
    <div class="media-content">
      <div class="content">
        <p>
          <strong><%= comment.name %>:</strong>
          <%= comment.comment %>
        </p>
      </div>
    </div>
     <%= link_to 'Delete', [comment.post, comment],
                  method: :delete, class: "button is-danger", data: { confirm: 'Are you sure?' } %>
  </article>

</div>
---
app/views/comments/_from.html.erb
---
<%= simple_form_for([@post, @post.comments.build]) do |f| %>

<div class="field">
  <div class="control">
    <%= f.input :name, input_html: { class: 'input' }, wrapper: false, label_html: { class: 'label' } %>
  </div>
</div>

<div class="field">
  <div class="control">
    <%= f.input :comment, input_html: { class: 'textarea' }, wrapper: false, label_html: { class: 'label' }  %>
  </div>
</div>
<%= f.button :submit, 'Leave a reply', class: "button is-primary" %>
<% end %>
---
```
# demo_blog 的最终效果
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsle85n6oj31kw0twtbo.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsldzv9xmj31kw0omdif.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsldrv83oj31kw0rdq57.jpg)
![image](https://ws1.sinaimg.cn/large/006tNc79gy1fpsldmrzi9j31kw0tf417.jpg)
