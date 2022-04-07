# yolo_ffmpeg_website


도커볼륨
https://www.daleseo.com/docker-volumes-bind-mounts/

Docker-Flask-간단한-추론-API-서버-띄우기
https://soundprovider.tistory.com/entry/Docker-Flask-%EA%B0%84%EB%8B%A8%ED%95%9C-%EC%B6%94%EB%A1%A0-API-%EC%84%9C%EB%B2%84-%EB%9D%84%EC%9A%B0%EA%B8%B0



image파일 도커에 pull 로 다운로드하고

컨테이너에 
(docker run -i -t --name ubuntu_test -v C:/test_final:/test_final ubuntu
예시인데 이말은 곧 ubuntu 이미지를 가져와서 my_vol 이라는 컨테이너를 생성하고 볼륨공유는 hostpc : test_2 에 ubuntu 이미지를 다운로드해라 라는말임.. 그러므로 삭제하면 다시 다 해야함 -p 해서 ip설정도 할수있다는데 아직 잘 모르겠음)

docker run -itd -v C:/test:/test ubuntu
이렇게 공유파일 설정한 상태임

docker 안에서 파이썬을 설치하기위해 
apt-get update
apt-get instsall -y python3 python3-pip
까지 한 상태

혹시나중에 flask까지 연동해서 사용한다면 
각종 library들이 설치될건데 그것도 적어놔야 나중에 docker file 로 정의할때 편리함.

pip install --upgrade pip && pip install flask
이것도하면 docker 내부에 flask 깔 수 있을듯

도커 복사붙여넣기 ctrl c ctrl v 마우스 우클릭





도커 네트워크 구조이해
https://captcha.tistory.com/70
(
- 도커는 컨테이너에 내부 IP를 순차적으로 할당
- 내부 IP는 컨테이너를 재시작할 때마다 변경될 수 있음
- 내부 IP는 도커가 설치된 호스트, 즉 내부망에서만 쓸 수 있는 IP이므로 외부와 연결될 필요가 있음 )



중요함!! : docker run -it -p 5000:5000 --name test_final -v C:/test_final:/test_final ubuntu:18.04

docker안에서 테스트하려면 test_final 컨테이너로 들어가야함

다시 처음부터 만들어보자용 ㅎㅎ
docker run -it -p 5000:5000 --name test_final -v C:/hostfolder명:/ubuntufolder명 ubuntu:18.04

이거쓰면될듯 ㅎㅎ...!!!!!!!
docker 파일 생성하고


이거 해봐야함

dockerfile 만드려면 파일명또한 dockerfile이여야함


yolov4 돌리기위한 과정

apt-get update &
apt-get upgrade &
apt-get install -y python3-pip &
apt-get install -y git &
apt-get install -y libjpeg-dev zlib1g-dev
(pillow설치를 위해)
apt-get install -y cmake
(opencv-python 에서 에러없애는 방법)

requirement 하기전에
이건 nano로 바꿔야할듯
pip3 install -U setuptools
( -U -> upgrade )
(pillow 설치오류남)
pip3 install scikit-build 이거해야함.

requirements.txt 에서 numpy 를 지우고 numpy==1.17을 그냥 numpy 로 바꿔야함

그다음
pip3 install -r -y requirements.txt




docker build -t final:fi .
docker build -t final:last .

docker build -t LoA:tag_name

docker file 만들고 그안에서 
docker build -t "test:v1" .
-> 이건 test image name에 v1 tag가 생김
이명령어 때리면 docker image가 만들어지는듯 ( 물론 따옴표는 떼야함! )
근데 이름이랑 서버가 어케지정되는지 모르겠음

docker run -it -p 5000:5000 --name test_final -v C:/hostfolder명:/ubuntufolder명 ubuntu:18.04

docker run -it -p 5000:5000 --name final -v C:/test_final:/test_final final:fi

이런식으로 image이름 , tag를 들고오면 되네



이미지:version

이렇게 하는게 정신건강에 편한듯


python3 test.py --img 640 --conf 0.001 --batch 8 --device 'cpu' --data /images/a.jpg --cfg cfg/yolov4-pacsp.cfg --weights weights/yolov4-csp-leaky.weights

일케하는데 unicode error남



ffmpeg -i myvideo.avi -vf fps=1/60 img%03d.jpg



----------------------------docker에서 gpu사용하기----------------------------------------

docker run --gpus all -i -t  --name final -v C:/docker:/docker holy:v

----------------------------docker에서 gpu사용하기----------------------------------------



------------------docker에서 gpu사용하고 메모리 16G 공유하기-------------------------------
(이렇게 안하면 나중에 docker 안에서 학습시킬때 메모리부족뜸)

docker run --gpus all -i -t  --name ti_test --shm-size=16G -v C:/tinaface/vedadet:/vedadet tinaface:ti

------------------docker에서 gpu사용하고 메모리 16G 공유하기-------------------------------


------------------docker에서 GUI program띄우기 ------------------------------------------

docker run -it --gpus all -v /tmp/.X11-unix:/tmp/.X11-unix -v C:/tinaface/vedadet:/vedadet --shm-size=16G -e DISPLAY=unix$DISPLAY --name ti_final tinaface:final
( 공유볼륨을 두개하고 싶을때 단순히 두번 불러주면 됨. )
( 현재는 컨테이너->이미지 변경 후 테스트 중 )

------------------docker에서 GUI program띄우기 ------------------------------------------
