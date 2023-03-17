# vim 한글 깨질 때 인코딩 방식 지정

뷰만 해결할 때는 커맨드에 `:set encoding=utf-8` (edit mode에서만 일시적으로 뷰가 깨지지 않음)\
vim 옵션으로서 계속 사용하려면 .vimrc 설정파일에 인코딩 방식 지정하는 코드 추가

1. vim /etc/vim/vimrc를 열어서
2.

```vim
set encoding=utf-8 
set fileencodings=utf-8,cp949
```



