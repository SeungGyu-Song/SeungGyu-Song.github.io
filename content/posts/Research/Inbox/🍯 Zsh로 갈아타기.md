---
title: <Fill me w/ a compact title>
draft: false
tags:
---
 
reference : 
1. [zsh 설치하는 velog 블로그](https://velog.io/@cosmos42/Ubuntu%EC%97%90-zsh-oh-my-zsh-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0)
2. [설치 맨 처음에 참고했던 블로그](https://velog.io/@hsk2454/%EB%A6%AC%EB%88%85%EC%8A%A4%EC%97%90-zshell-%EC%84%A4%EC%B9%98-%EB%B0%8F-oh-my-zsh%EB%A1%9C-%ED%85%8C%EB%A7%88-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0)


## zsh 및 oh-my-zsh 설치
``` sh
sudo apt-get install zsh  # zsh설치
zsh --version   #버전체크
chsh -s /usr/bin/zsh  # zsh을 기본 shell로 저장

```

리눅스를 log out했다가 다시 들어오고 터미널을 키면 
“This is the Z Shell configuration function for new users, …” 하면서 문구가 나오는데 oh-my-zsh로 테마 설정을 해줄 거니까 q를 눌러서 빠져나오자.

```sh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
#oh-my-shell 설치.
```

[zsh theme 사이트](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)에서 좋은 테마 찾아서 
`gedit ~/.zshrc` 후, “ZSH_THEME” 찾아서 이름을 넣어놓자.


## Conda 잡아주기
우선 원래 bashrc로 들어가서 conda의 위치를 확인한다. (`/home/snggu/anaconda3/bin/conda)

그리고 아래 명령어로 conda init
```sh
/home/snggu/anaconda3/bin/conda init zsh
```

### 1. zsh-syntax highlighting
```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### 2. zsh-auto-suggestions
```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

이후 `gedit ~/.zshrc`로 들어가서 plugin