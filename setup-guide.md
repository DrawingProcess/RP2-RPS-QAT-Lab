# 개발환경 설정 가이드

이 문서는 `RP2-RPS-QAT-Lab` 실습용 개발환경을 빠르게 만드는 방법을 정리한 파일입니다.

## 1. 대상

- GCP GPU 서버에 접속해서 VSCode로 실습하는 학생
- `RPS_QAT_DenseNet121_초보자용.ipynb` 또는 `RPS_QAT_ResNet50_초보자용.ipynb`를 실행할 학생

## 2. 준비물

- Git
- Python 3.10 이상
- VSCode
- 저장소 복제본

## 3. 가상환경 만들기

저장소 루트에서 아래 순서로 실행합니다.

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
```

## 4. 패키지 설치

실습에 필요한 기본 패키지를 설치합니다.

```bash
python -m pip install jupyter ipykernel tensorflow tensorflow-model-optimization opencv-python-headless scikit-learn matplotlib
```

노트북 커널로 등록하면 VSCode에서 선택하기 쉽습니다.

```bash
python -m ipykernel install --user --name rp2-rps-qat-lab --display-name "Python (rp2-rps-qat-lab)"
```

## 5. VSCode에서 확인

1. 저장소를 VSCode로 엽니다.
2. 노트북 파일을 연 뒤 커널을 `.venv` 또는 `Python (rp2-rps-qat-lab)`으로 바꿉니다.
3. 첫 셀을 실행해서 `tensorflow`, `opencv`, `scikit-learn` import가 되는지 확인합니다.

## 6. 자주 쓰는 점검 명령

```bash
which python
python --version
python -m pip list | head
```

GPU 서버인지 확인할 때는 아래를 사용합니다.

```bash
nvidia-smi
```

## 7. 문제 해결

- `ModuleNotFoundError`가 나면 가상환경이 활성화되었는지 먼저 확인합니다.
- 커널이 보이지 않으면 `ipykernel` 설치 후 VSCode를 다시 열어봅니다.
- GPU가 안 보이면 서버 접속 상태와 `nvidia-smi` 결과를 먼저 확인합니다.

## 8. 사용 순서 요약

1. 저장소 clone
2. `.venv` 생성
3. 패키지 설치
4. 커널 등록
5. VSCode에서 노트북 실행
