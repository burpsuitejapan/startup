# 4 �f�f���@�ɂ���
## 4.1 Proxy�@�\
### 4.1.1 Proxy�𗘗p�����ʐM�L���v�`��
��ʓI�ȃN���C�A���gProxytool�Ɋւ������  
MITM����Ă���悤�Ȃ����܂�̊G�Ɠ��e�����������C���[�W  
���邾������Ȃ��ĕύX���ł����BSSL���C�P�܂���B�݂����Ȃ��Ƃ������B

### 4.1.2 Proxy�^�u�̍\��
Proxy�^�u���\������e�^�u�Ɋւ���ȒP�ȊT�v�̐���  
- Intercept
- HTTP history
- WebSockets history
- Options
 
## 4.2 Burp Suite�ɂ��ʐM�̃L���v�`��
### 4.2.1 �ʐM���L���v�`�����Ă݂悤�I
1. �u���E�U�ŃA�N�Z�X����(�����̎��ȉ���_�̐ݒ�󋵂��m�F)
  - �u���E�U���ŁA3�͂Ő�������Proxy�ݒ肪����Ă��邱��
  - �uIntercept�v�^�u���uIntercept is off�v�Ɛݒ肳��Ă��邱��
2. �uHTTP hisotry�v�^�u�ŒʐM���e���{��  
  �uHTTP hisotry�v�^�u�̉�ʍ\���y�ь����ɂ��Đ���  
  �㕔�t�B�[���h�ɂ��Ă̐���(�ȉ��̏�񂪕\������Ă���)
    - Host
    - Method
    - URL
    - Params
    - Edited
    - Status
    - Length
    - MIME type
    - Extension
    - title
    - Comment
    - SSL
    - IP
    - Cookies
    - Time
    - Listener port

  �I������Ɖ����^�u��Request��Pesponse�f�[�^�̏ڍׂ��{���ł���  
  �����^�u�̏ڍׂɂ��Đ���(Request�^�u�� Pesponse�^�u)  
  �ȉ��^�u�ɂč��ڂ��ƂɃf�[�^��\���\
    - Raw
    - Params
    - Headers
    - Hex

  Filetr�@�\�̐���

### 4.2.2 �l�����������đ��M���Ă݂悤�I
1. �u���E�U�ŃA�N�Z�X����(�����̎��ȉ���_�̐ݒ�󋵂��m�F)
  - �u���E�U���ŁA3�͂Ő�������Proxy�ݒ肪����Ă��邱��
  - �uIntercept�v�^�u���uIntercept is on�v�Ɛݒ肳��Ă��邱��
2. �uIntercept�v�^�u�Œl��ύX  
�uIntercept�v�^�u�̉�ʍ\���y�ь����ɂ��Đ���
  - �㕔�{�^��
    - Forward
    - Drop
    - Intercept on or off
    - Action
  - �����^�u
    - Raw
    - Params
    - Headers
    - Hex
3. �uHTTP hisotry�v�^�u�Ō��ʂ��{��  
�uEdited request�v�̃^�u�Ɋւ������    
request��������Ȃ���response�̃C���^�[�Z�v�g�ɂ��Ă��⑫����

## 4.3 ���̑�

### 4.3.1 ���N�G�X�g�̍đ��M

Repeater�̎g����

### 4.3.2 Scope�ݒ�

�X�R�[�v�ݒ�̕K�v�����B

### 4.3.3 �T�[�o�ؖ����ݒ�

�T�[�o�ؖ����̐ݒ肪�K�v�ȗ��R

- �Í����ʐM�T�C�g�ɃA�N�Z�X����ƃG���[���������ĉ�ʂ��\������Ȃ�
-- BurpSuite�́u�I���I���ؖ����v���u���E�U�ɒe�����

1.Burp����擾�����ؖ������u���E�U�ɃC���|�[�g


### 4.3.4 ���O�ۑ��ݒ�

1.[Options]-[Misc]-Logging]�̐ݒ�
ALL��Tools�̎g�������ARequest��Response
�Q�l���Ƃ���Logger++�ւ̃|�C���^

### 4.3.5 �A�b�v�X�g���[��Proxy�ݒ�
1.�w�i
- �Г�Proxy�̐}

2.�ݒ�
- �}�ɋ�̓I�Ȑݒ�l����ꂽ���̂�������
-- Desitination Host��*(���C���h�J�[�h)�����b�͕K�{
-- �F�ؕ����AID/PWD

3.�A�b�v�X�g���[��Proxy���p���̍l���_�Ƒ΍�
- ���O�����x���Ȃ��� 
- Connection timeout�܂��Œx�����

### 4.3.6 Intruder
1.�蓮�f�f���h��
- �T�O�}

2.�g����
- 
- Automatic Payload Position

3.�A�b�v�X�g���[��Proxy���p���̍l���_�Ƒ΍�
- ���O�����x���Ȃ��� 
- Connection timeout�܂��Œx�����


��ԃx�[�V�b�N�Ȏg�����B���ʂ̌������BGrep match���ꂽ���B

### 4.3.7 Extender

Extender���ǂ��������̂��B�ǂ��������Ƃ��ł���̂��B
