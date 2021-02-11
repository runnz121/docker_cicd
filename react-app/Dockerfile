FROM node:alpine as builder 
#여기 from부터 다음 from까지 모두 builder stage 라는 것을 명시 

WORKDIR '/usr/src/app'

COPY package.json .

RUN npm install

COPY ./ ./

RUN npm run build

#--builder state : 이곳의 목표는 빌드파일들을 생성하는것 생성된 파일과 폴더들은
# 모두 /usr/src/app/build로 들어간다 


#run state 
FROM nginx
COPY --from=builder /usr/src/app/build /usr/share/ngnix/html 
#--from=builder : 다른 stage에 있는 파일을 복사할 때 다른 stage 이름을 명시
# /usr/src/app/build /usr/share/ngnix/html :
#builder stage에서 생성된 파일들은 /usr/src/app/build 에 들어가게 되며
#그곳에저장된 파일들을 /usr/share/ngnix/html 로 복사 시켜줘서
#ngnix가 웹 브라우저의 http요청이 올 때마다 알맞은 파일을 전해 줄수 있게 함
#/usr/share/ngnix/html 이 장소로 build 파일들을 복사 시켜주는 이유는
# 이 장소로 파일을 넣어 두면 ngnix가 알아서 client 요청이 들어올 때 알맞은 정적 파일
#들을 제공해줌 : 이장소는 설정을 통해 바꿀 수 있다. 

#docker build . 
#docker run -p 8080:80 runnz121/docker-react-app :일반적으로 ngnix는 80포트 사용 