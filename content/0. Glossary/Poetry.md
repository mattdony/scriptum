- 가상환경 생성위치 설정하기
	```zsh
	potery config --list

	poetry config virtualenvs.in-project true
	poetry config virtualenv.path "./.venv"
	```
- `poetry shell`명령어를 통해 가상환경 생성시 프로젝트 내부에 `.venv`폴더에 가상환경이 생성되는 것을 확인할 수 있음
- 가상환경 접속시 터미널에는 poetry의 기본값인 `{project_name}-py{python_version}`로 표기된다.

