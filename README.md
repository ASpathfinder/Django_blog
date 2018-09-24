# Django_blog

```
import markdown
from django.shortcuts import render, get_object_or_404
from django.http import HttpResponse
from .models import Post, Category, Tag
from comments.forms import CommentForm
from django.contrib import admin
from django.db.models import Q

def index(request):
    post_list = Post.objects.all().order_by('-created_time')
    for post in post_list:
        post.get_comment_time()
    

    return render(request, 'blog/index.html', context={
                'title': '我的博客首页',
                'welcome': '欢迎访问我的博客首页',
                'post_list': post_list
            }) 


def detail(request, pk):
    post = get_object_or_404(Post, pk=pk)
    post.add_views()
    post.body = markdown.markdown(post.body, extensions=[
                    'markdown.extensions.extra',
                    'markdown.extensions.codehilite',
                    'markdown.extensions.toc',
                    ])
    post.get_comment_time()
    form = CommentForm()
    comment_list = post.comment_set.all()
    category_list = Category.objects.all()
    tag_list = Tag.objects.all()
    return render(request, 'blog/detail.html', context={
        'post': post,
        'pk': pk,
        'form': form,
        'comment_list': comment_list,
        'category_list': category_list,
        'tag_list': tag_list
        })

def article(request):
    post_list = Post.objects.all().order_by('-created_time')
    for post in post_list:
        post.get_comment_time()

    category_list = Category.objects.all()
    tag_list = Tag.objects.all()
    error_msg = ''
    return render(request, 'blog/article.html', context= {
        'post_list': post_list,
        'category_list': category_list,
        'tag_list': tag_list,
        'error_msg': error_msg
        })

def archives(request, pk):
    post_list = Post.objects.filter(
            category__pk=pk
            ).order_by('-created_time')
    for post in post_list:
        post.get_comment_time()
    
    tag_list = Tag.objects.all()
    category_list = Category.objects.all()
    return render(request, 'blog/article.html', context= {
        'post_list': post_list,
        'category_list': category_list,
        'tag_list': tag_list
        })

def archives_ym(request, year, month):
    post_list = Post.objects.filter(
            created_time__year=year,
            created_time__month=month
            ).order_by('-created_time')
    for post in post_list:
        post.get_comment_time()
    
    tag_list = Tag.objects.all()
    category_list = Category.objects.all()
    return render(request, 'blog/article.html', context= {
        'post_list': post_list,
        'category_list': category_list,
        'tag_list': tag_list
        })


def tags(request, pk):
    post_list = Post.objects.filter(
            tags__pk=pk
            ).order_by('-created_time')
    for post in post_list:
        post.get_comment_time()

    tag_list = Tag.objects.all()
    category_list = Category.objects.all()
    return render(request, 'blog/article.html', context= {
        'post_list': post_list,
        'category_list': category_list,
        'tag_list': tag_list
        })

def search(request):
    keywords = request.GET.get('keywords')
    error_msg = ''
    error_banner = ''
    category_list = Category.objects.all()
    tag_list = Tag.objects.all()
    if not keywords:
        error_banner = '请输入关键词'
        error_msg = 'nothing'
        post_list = Post.objects.all().order_by('-created_time')
        for post in post_list:
            post.get_comment_time()

        return render(request, 'blog/article.html', {'error_msg': error_msg,
                                                     'error_banner': error_banner,
                                                     'post_list': post_list,
                                                     'category_list': category_list,
                                                     'tag_list': tag_list
                                                     })
    
    post_list = Post.objects.filter(Q(title__icontains=keywords) | Q(body__icontains=keywords))
    for post in post_list:
        post.get_comment_time()

    if not post_list.exists():
        error_msg = 'nothing'
        error_banner= '未搜索到与' + ' \'' + keywords + '\' ' + '有关的文章，随便看看吧！'
    
    return render(request, 'blog/article.html', {'error_msg': error_msg,
                                                'post_list': post_list,
                                                'category_list': category_list,
                                                'tag_list': tag_list,
                                                'error_banner': error_banner
                                               })


def about(request):
    return render(request, 'blog/about.html')

```
