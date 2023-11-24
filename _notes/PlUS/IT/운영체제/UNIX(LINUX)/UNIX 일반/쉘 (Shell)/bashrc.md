  
- bash에서 작업할 때마다 수행되는 파일로서, 우리가 그냥 python이라고 입력만 해도 python3.x버전으로 연결되어 작업할 수 있게 해줌. 
- 즉 환경변수 개념이라고 생각하면 편하다. 만약 모든 사용자에게 적용되게 하려면 /etc/profile에 설정해주면 됨.
- 개별 사용자에게 적용되게 하려면 .bash에 설정.
- .bashrc는 bash이 실행될 때마다 수행되고, .bash_profile은 bash이 login shell로 쓰일 때(즉 처음 login할 때)에 수행됨.