---
layout: post
title: "Changes to Controller Testing in Rails 5"
categories:
- development
- rails
date: 2016-04-25T14:56:47+06:30
external_url: http://blog.bigbinary.com/2016/04/19/changes-to-test-controllers-in-rails-5.html
---

With upcoming rails 5 release, here are the changes one needs to take note of in testing controllers.

<!--more-->

## `ActionController::TestCase` is deprecated

`ActionDispatch::IntegrationTest` is the new replacement.

## Call the urls instead of request methods in Rails 5

**Then**:

```
class ProductsControllerTest < ActionController::TestCase


  def test_index_response
    get :index
    assert_response :success
  end
end
```

**Now**:

```
class ProductsControllerTest < ActionDispatch::IntegrationTest


  def test_index
    get products_url
    assert_response :success
  end
end
```

## You can no longer test using `assigns` and `assert_template`

Apparently they are no longer the rails way of testing things as [the venerable @dhh has discussed in length.](https://github.com/rails/rails/issues/18950)


There's a gem called [rails-controller-testing](https://github.com/rails/rails-controller-testing) that's extracted though if you wish to continue using them.

## You can use keyword arguments in HTTP request methods

Then:

```
class ProductsControllerTest < ActionController::TestCase


  def test_show
    get :show, { id: user.id }, { notice: 'Welcome' }, { admin: user.admin? }
    assert_response :success
  end
end

```

Now:

```
class ProductsControllerTest < ActionDispatch::IntegrationTest


  def test_create
    post product_url, params: { product: { name: "FIFA" } }
    assert_response :success
  end
end
```

