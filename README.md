# RP2-RPS-QAT-Lab

학생용 가위바위보(Rock/Paper/Scissors) QAT 실습 저장소입니다.

이 저장소는 전체 강의자료가 아니라 오늘 실습에 필요한 파일만 포함합니다.

## 포함 파일

```text
RP2-RPS-QAT-Lab/
  README.md
  setup-guide.md
  RPS_Dataset/
    0/  scissors
    1/  rock
    2/  paper
  notebooks/
    RPS_Classification_DenseNet121_지난주실습.ipynb
    RPS_QAT_DenseNet121_초보자용.ipynb
    RPS_QAT_ResNet50_초보자용.ipynb
  .gitignore
```

## 실습 목표

- GitHub 저장소를 fork한다.
- GCP GPU 서버에 VSCode로 접속한다.
- 자신의 fork 저장소를 clone한다.
- RPS 이미지 데이터셋으로 가위/바위/보 분류 모델을 학습한다.
- QAT(Quantization Aware Training)를 적용한다.
- 라즈베리파이에서 사용할 수 있는 `.tflite` 모델을 만든다.

## 1. Fork

아래 원본 저장소를 자신의 GitHub 계정으로 fork합니다.

```text
https://github.com/philipdekim-OnD01/RP2-RPS-QAT-Lab
```

fork 후 자신의 저장소 주소는 보통 다음 형태입니다.

```text
https://github.com/학생아이디/RP2-RPS-QAT-Lab.git
```

## 2. GCP GPU 서버에서 clone

VSCode Remote SSH로 GCP GPU 서버에 접속한 뒤 터미널에서 실행합니다.

```bash
mkdir -p ~/workspace
cd ~/workspace
git clone https://github.com/학생아이디/RP2-RPS-QAT-Lab.git
cd RP2-RPS-QAT-Lab
code .
```

GPU가 보이는지 확인합니다.

```bash
nvidia-smi
```

## 3. Python 환경 준비

상세한 개발환경 설정은 `setup-guide.md`를 따릅니다.

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install jupyter ipykernel tensorflow tensorflow-model-optimization opencv-python-headless scikit-learn matplotlib
```

VSCode에서 노트북 커널을 `.venv`로 선택합니다.

## 4. 실행할 노트북

지난주 기본 실습:

```text
notebooks/RPS_Classification_DenseNet121_지난주실습.ipynb
```

기본 권장:

```text
notebooks/RPS_QAT_DenseNet121_초보자용.ipynb
```

비교 실습:

```text
notebooks/RPS_QAT_ResNet50_초보자용.ipynb
```

지난주 기본 실습을 먼저 확인한 뒤, DenseNet121 QAT 버전과 ResNet50 QAT 버전을 비교하는 것을 권장합니다.

## 5. 데이터셋 경로

노트북은 저장소 루트의 `RPS_Dataset` 폴더를 자동으로 찾습니다.

정상 실행 시 다음과 비슷한 출력이 나옵니다.

```text
RPS dataset path: .../RP2-RPS-QAT-Lab/RPS_Dataset
Class folders: ['0', '1', '2']
```

## 6. 결과 파일

학습 결과는 `results/` 폴더에 저장됩니다.

```text
results/
  RPS_PreTrained_DenseNet.keras
  RPS_PreTrained_DenseNet.tflite
  RPS_PreTrained_DenseNet_Augmentation_QAT.h5
  RPS_PreTrained_DenseNet_Augmentation_QAT.tflite
```

또는 ResNet50 버전에서는 다음 파일이 생성됩니다.

```text
results/
  RPS_PreTrained_ResNet50_Augmentation_QAT.h5
  RPS_PreTrained_ResNet50_Augmentation_QAT.tflite
```

`results/`는 `.gitignore`에 포함되어 있으므로 큰 모델 파일이 실수로 GitHub에 올라가지 않습니다.

## 7. GitHub에 결과 push

노트북 수정 내용이나 README만 push합니다.

```bash
git status
git add notebooks README.md
git commit -m "Run RPS QAT lab on GCP GPU"
git push origin main
```

대용량 모델 파일(`.h5`, `.keras`, `.tflite`, `.zip`)은 GitHub에 올리지 않습니다.

## 8. 제출 또는 확인 항목

- 자신의 fork 저장소 URL
- `nvidia-smi` 실행 화면
- 노트북에서 `RPS_Dataset` 경로가 정상 출력된 화면
- 학습 accuracy와 validation accuracy
- 생성된 `.tflite` 파일명
- push한 commit URL
