# Gitѧϰ

## ��������
+ �����ļ����ļ���
  1. <font color=OrangeRed>cd</font> �ı�Ŀ¼�����л����ĸ�Ŀ¼��
  2. <font color=OrangeRed>cd ..</font> ���˵���һ��Ŀ¼��ע��cd��..֮���пո�
  3. <font color=OrangeRed>pwd</font> ��ӡ����Ŀ¼��������ʾ��ǰ�����ļ���Ŀ¼·��
  4. <font color=OrangeRed>ls</font> �г���ǰĿ¼�������ļ�
  5. <font color=OrangeRed>touch</font> �½�һ���ļ���
  6. <font color=OrangeRed>rm</font> ɾ��һ���ļ�
  7. <font color=OrangeRed>mkdir</font> �½�һ��Ŀ¼�����½�һ���ļ���
  8. <font color=OrangeRed>rm -r</font> ɾ��һ���ļ���
  9. <font color=OrangeRed>mv</font> �ƶ��ļ�
  10. <font color=OrangeRed>reset</font> ����
+ �½������
  1. <font color=OrangeRed>git init</font> �ڵ�ǰĿ¼�½�һ��git�����
  2. <font color=OrangeRed>git init [�ļ���]</font> �½�һ��Ŀ¼�������ʼ��Ϊgit�����
  3. <font color=OrangeRed>git clone [��Ŀ��ַ]</font> ����һ����Ŀ����������������ʷ
+ ����
  1. <font color=OrangeRed>git config --list</font> ��ʾ��ǰgit����
  2. <font color=OrangeRed>git config -e [--global]</font> �༭git�����ļ�
  3. <font color=OrangeRed>git config [--global] user.name "[�û���]"</font> ����git�û���
  4. <font color=OrangeRed>git config [--global] user.email "[�û�����]"</font> ����git�ʼ���ַ
+ ����/ɾ���ļ�
  1. <font color=OrangeRed>git add [�ļ���1] [�ļ���2] ...</font> ���ָ���ļ����ݴ���
  2. <font color=OrangeRed>git add [ָ��Ŀ¼]</font> ���ָ��Ŀ¼���ݴ�����������Ŀ¼
  3. <font color=OrangeRed>git add .</font> ��ӵ�ǰĿ¼�������ļ����ݴ���
  4. <font color=OrangeRed>git add -p</font> ���ÿ���仯ǰ������Ҫ��ȷ�ϣ�����һ���ļ��Ķദ�仯����ʵ�ֲַ��ύ
  5. <font color=OrangeRed>git rm [�ļ���1] [�ļ���2] ...</font> ɾ���������ļ������ҽ��˴�ɾ�������ݴ���
  6. <font color=OrangeRed>git rm --cached [�ļ�]</font> ֹͣ׷��ָ���ļ��������ļ��ᱣ���ڹ�����
  7. <font color=OrangeRed>git mv [ԭ�ļ���] [���ļ���]</font> ���ļ���������������������ݴ���
+ �����ύ
  1. <font color=OrangeRed>git commit -m [message]</font> �ύ�ݴ������ֿ���
  2. <font color=OrangeRed>git commit [file1] [file2] ... -m [message]</font> �ύ�ݴ�����ָ���ļ����ֿ���
  3. <font color=OrangeRed>git commit -a</font> �ύ���������ϴ�commit֮��ı仯��ֱ�ӵ��ֿ���
  4. <font color=OrangeRed>git commit -v</font> �ύʱ��ʾ����diff��Ϣ
  5. <font color=OrangeRed>git commit -am [message]</font> ��add��commit��Ϊһ��
  6. <font color=OrangeRed>git commit --amend -m [message]</font> ʹ��һ���µ�commit�������һ���ύ,�������û���κ��±仯����������д��һ��commit���ύ��Ϣ
  7. <font color=OrangeRed>git commit --amend [file1] [file2] ...</font> ������һ��commit��������ָ���ļ����±仯
+ ��֧
  1. <font color=OrangeRed>git branch</font> �г����б��ط�֧
  2. <font color=OrangeRed>git branch -r</font> �г�����Զ�̷�֧
  3. <font color=OrangeRed>git branch -a</font> �г����б��ط�֧��Զ�̷�֧
  4. <font color=OrangeRed>git branch [branch-name]</font> �½�һ����֧������Ȼͣ���ڵ�ǰ��֧
  5. <font color=OrangeRed>git checkout -b [branch]</font> �½�һ����֧�����л����÷�֧
  6. <font color=OrangeRed>git branch [branch] [commit]</font> �½�һ����֧��ָ��ָ��commit
  7. <font color=OrangeRed>git branch --track [branch] [remote-branch]</font> �½�һ����֧����ָ����Զ�̷�֧����׷�ٹ�ϵ
  8. <font color=OrangeRed>git checkout [branch-name]</font> �л���ָ����֧�������¹�����
  9. <font color=OrangeRed>git checkout -</font> �л�����һ����֧
  10.<font color=OrangeRed>git branch --set-upstream [branch] [remote-branch]</font> ����׷�ٹ�ϵ�������з�֧��ָ����Զ�̷�֧֮��
  11. <font color=OrangeRed>git merge [branch]</font> �ϲ�ָ����֧����ǰ��֧
  12. <font color=OrangeRed>git cherry-pick [commit]</font> ѡ��һ��commit���ϲ�����ǰ��֧
  13. <font color=OrangeRed>git branch -d [branch-name]</font> ɾ����֧
  14. <font color=OrangeRed>git push origin --delete [branch-name]</font> ɾ��Զ�̷�֧
  15. <font color=OrangeRed>git branch -dr [remote/branch]</font> ɾ��Զ�̷�֧
  16. <font color=OrangeRed>git checkout v2.0</font> ����汾v2.0
  17. <font color=OrangeRed> checkout -b devel origin/develop</font> ��Զ�̷�֧develop�����±��ط�֧devel�����
  18. <font color=OrangeRed> checkout -- README</font> ���head�汾��README�ļ����������޸Ĵ�����ˣ�
+ ��ǩ
  1. <font color=OrangeRed>git tag</font> �г�����tag
  2. <font color=OrangeRed>git tag [tag]</font> �½�һ��tag�ڵ�ǰcommit
  3. <font color=OrangeRed>git tag [tag]</font> [commit] �½�һ��tag��ָ��commit
  4. <font color=OrangeRed>git tag -d [tag]</font> ɾ������tag
  5. <font color=OrangeRed>git push origin :refs/tags/[tagName]</font> ɾ��Զ��tag
  6. <font color=OrangeRed>git show [tag]</font> �鿴tag��Ϣ
  7. <font color=OrangeRed>git push [remote] [tag]</font> �ύָ��tag
  8. <font color=OrangeRed>git push [remote] --tags</font> �ύ����tag
  9. <font color=OrangeRed>git checkout -b [branch] [tag]</font> �½�һ����֧��ָ��ĳ��tag
+ �鿴��Ϣ
  1. <font color=OrangeRed>git status</font> ��ʾ�б�����ļ�
  2. <font color=OrangeRed>git log</font> ��ʾ��ǰ��֧�İ汾��ʷ
  3. <font color=OrangeRed>git log --stat</font> ��ʾcommit��ʷ���Լ�ÿ��commit����������ļ�
  4. <font color=OrangeRed>git log -S [keyword]</font> �����ύ��ʷ�����ݹؼ���
  5. <font color=OrangeRed>git log [tag] HEAD --pretty=format:%s</font> ��ʾĳ��commit֮������б䶯��ÿ��commitռ��һ��
  6. <font color=OrangeRed>git log [tag] HEAD --grep feature</font> ��ʾĳ��commit֮������б䶯����"�ύ˵��"���������������
  7. <font color=OrangeRed>git log --follow [file]</font> ��ʾĳ���ļ��İ汾��ʷ�������ļ�����
  8. <font color=OrangeRed>git whatchanged [file]</font> ��ʾĳ���ļ��İ汾��ʷ�������ļ�����
  9. <font color=OrangeRed>git log -p [file]</font> ��ʾָ���ļ���ص�ÿһ��diff
  10. <font color=OrangeRed>git log -5 --pretty --oneline</font> ��ʾ��ȥ5���ύ
  11. <font color=OrangeRed>git shortlog -sn</font> ��ʾ�����ύ�����û������ύ��������
  12. <font color=OrangeRed>git blame [file]</font> ��ʾָ���ļ���ʲô����ʲôʱ���޸Ĺ�
  13. <font color=OrangeRed>git diff</font> ��ʾ�ݴ����͹������Ĳ���
  14. <font color=OrangeRed>git diff --cached [file]</font> ��ʾ�ݴ�������һ��commit�Ĳ���
  15. <font color=OrangeRed>git diff HEAD</font> ��ʾ�������뵱ǰ��֧����commit֮��Ĳ���
  16. <font color=OrangeRed>git diff [first-branch]...[second-branch]</font> ��ʾ�����ύ֮��Ĳ���
  17. <font color=OrangeRed>git diff --shortstat "@{0 day ago}"</font> ��ʾ������д�˶����д���
  18. <font color=OrangeRed>git show [commit]</font> ��ʾĳ���ύ��Ԫ���ݺ����ݱ仯
  19. <font color=OrangeRed>git show --name-only [commit]</font> ��ʾĳ���ύ�����仯���ļ�
  20. <font color=OrangeRed>git show [commit]:[filename]</font> ��ʾĳ���ύʱ��ĳ���ļ�������
  21. <font color=OrangeRed>git reflog</font> ��ʾ��ǰ��֧����������ύ
+ Զ��ͬ��
  1. <font color=OrangeRed>git fetch [remote]</font> ����Զ�ֿ̲�����б䶯
  2. <font color=OrangeRed>git remote -v</font> ��ʾ����Զ�ֿ̲�
  3. <font color=OrangeRed>git remote show [remote]</font> ��ʾĳ��Զ�ֿ̲����Ϣ
  4. <font color=OrangeRed>git remote add [shortname] [url]</font> ����һ���µ�Զ�ֿ̲⣬������
  5. <font color=OrangeRed>git pull [remote] [branch]</font> ȡ��Զ�ֿ̲�ı仯�����뱾�ط�֧�ϲ�
  6. <font color=OrangeRed>git push [remote] [branch]</font> �ϴ�����ָ����֧��Զ�ֿ̲�
  7. <font color=OrangeRed>git push [remote] --force</font> ǿ�����͵�ǰ��֧��Զ�ֿ̲⣬��ʹ�г�ͻ
  8. <font color=OrangeRed>git push [remote] --all</font> �������з�֧��Զ�ֿ̲�
+ ����
  1. <font color=OrangeRed>git checkout [file]</font> �ָ��ݴ�����ָ���ļ���������
  2. <font color=OrangeRed>git checkout [commit] [file]</font> �ָ�ĳ��commit��ָ���ļ����ݴ����͹�����
  3. <font color=OrangeRed>git checkout .</font> �ָ��ݴ����������ļ���������
  4. <font color=OrangeRed>git reset [file]</font> �����ݴ�����ָ���ļ�������һ��commit����һ�£�������������
  5. <font color=OrangeRed>git reset --hard</font> �����ݴ����빤����������һ��commit����һ��
  6. <font color=OrangeRed>git reset [commit]</font> ���õ�ǰ��֧��ָ��Ϊָ��commit��ͬʱ�����ݴ�����������������
  7. <font color=OrangeRed>git reset --hard [commit]</font> ���õ�ǰ��֧��HEADΪָ��commit��ͬʱ�����ݴ����͹���������ָ��commitһ��
  8. <font color=OrangeRed>git reset --keep [commit]</font> ���õ�ǰHEADΪָ��commit���������ݴ����͹���������
  9. <font color=OrangeRed>git revert [commit]</font> �½�һ��commit����������ָ��commit�����ߵ����б仯������ǰ�ߵ���������Ӧ�õ���ǰ��֧
  10. <font color=OrangeRed>git stash</font> ��ʱ��δ�ύ�ı仯�Ƴ����Ժ�������
  11. <font color=OrangeRed>git stash pop</font>
+ ����
  1. <font color=OrangeRed>git init</font>  ��ʼ������git�ֿ⣨�����²ֿ⣩
  2. <font color=OrangeRed>git config --global user.name "xxx"</font>  �����û���
  3. <font color=OrangeRed>git config --global user.email "xxx@xxx.com"</font>  �����ʼ�
  4. <font color=OrangeRed>git config --global color.ui true  git status</font>�������Զ���ɫ
  5. <font color=OrangeRed>git config --global color.status auto</font>
  6. <font color=OrangeRed>git config --global color.diff auto</font>
  7. <font color=OrangeRed>git config --global color.branch auto</font>
  8. <font color=OrangeRed>git config --global color.interactive auto</font>
  9. <font color=OrangeRed>git config --global --unset http.proxy  remove  proxy configuration on git</font>
  10. <font color=OrangeRed>git clone git+ssh://git@192.168.53.168/VT.git</font>  cloneԶ�ֿ̲�
  11. <font color=OrangeRed>git status</font>  �鿴��ǰ�汾״̬���Ƿ��޸ģ�
  12. <font color=OrangeRed>git add xyz</font>  ���xyz�ļ���index
  13. <font color=OrangeRed>git add .</font>  ���ӵ�ǰ��Ŀ¼�����и��Ĺ����ļ���index
  14. <font color=OrangeRed>git commit -m 'xxx'</font>  �ύ
  15. <font color=OrangeRed>git commit --amend -m 'xxx'</font>  �ϲ���һ���ύ�����ڷ����޸ģ�
  16. <font color=OrangeRed>git commit -am 'xxx'</font>  ��add��commit��Ϊһ��
  17. <font color=OrangeRed>git rm xxx</font>  ɾ��index�е��ļ�
  18. <font color=OrangeRed>git rm -r *</font>  �ݹ�ɾ��
  19. <font color=OrangeRed>git log</font>  ��ʾ�ύ��־
  20. <font color=OrangeRed>git log -1</font>  ��ʾ1����־ -nΪn��
  21. <font color=OrangeRed>git log -5</font>
  22. <font color=OrangeRed>git log --stat</font>  ��ʾ�ύ��־����ر䶯�ļ�
  23. <font color=OrangeRed>git log -p -m</font>
  24. <font color=OrangeRed>git show dfb02e6e4f2f7b573337763e5c0013802e392818</font>  ��ʾĳ���ύ����ϸ����
  25. <font color=OrangeRed>git show dfb02</font>  ��ֻ��commit id��ǰ��λ
  26. <font color=OrangeRed>git show HEAD</font>  ��ʾHEAD�ύ��־
  27. <font color=OrangeRed>git show HEAD^</font>  ��ʾHEAD�ĸ�����һ���汾�����ύ��־ ^^Ϊ�������汾 ^5Ϊ��5���汾
  28. <font color=OrangeRed>git tag</font>  ��ʾ�Ѵ��ڵ�tag
  29. <font color=OrangeRed>git tag -a v2.0 -m 'xxx'</font>  ����v2.0��tag
  30. <font color=OrangeRed>git show v2.0</font>  ��ʾv2.0����־����ϸ����
  31. <font color=OrangeRed>git log v2.0</font>  ��ʾv2.0����־
  32. <font color=OrangeRed>git diff</font>  ��ʾ����δ�����index�ı��
  33. <font color=OrangeRed>git diff --cached</font>  ��ʾ���������index����δcommit�ı��
  34. <font color=OrangeRed>git diff HEAD^</font>  �Ƚ�����һ���汾�Ĳ���
  35. <font color=OrangeRed>git diff HEAD -- ./lib</font>  �Ƚ���HEAD�汾libĿ¼�Ĳ���
  36. <font color=OrangeRed>git diff origin/master..master</font>  �Ƚ�Զ�̷�֧master���б��ط�֧master��û�е�
  37. <font color=OrangeRed>git diff origin/master..master --stat</font>  ֻ��ʾ������ļ�������ʾ��������
  38. <font color=OrangeRed>git remote add origin git+ssh://git@192.168.53.168/VT.git</font>  ����Զ�̶��壨����push/pull/fetch��
  39. <font color=OrangeRed>git branch</font>  ��ʾ���ط�֧
  40. <font color=OrangeRed>git branch --contains 50089</font>  ��ʾ�����ύ50089�ķ�֧
  41. <font color=OrangeRed>git branch -a</font>  ��ʾ���з�֧
  42. <font color=OrangeRed>git branch -r</font>  ��ʾ����ԭ����֧
  43. <font color=OrangeRed>git branch --merged</font>  ��ʾ�����Ѻϲ�����ǰ��֧�ķ�֧
  44. <font color=OrangeRed>git branch --no-merged</font>  ��ʾ����δ�ϲ�����ǰ��֧�ķ�֧
  45. <font color=OrangeRed>git branch -m master master_copy</font>  ���ط�֧����
  46. <font color=OrangeRed>git checkout -b master_copy</font>  �ӵ�ǰ��֧�����·�֧master_copy�����
  47. <font color=OrangeRed>git checkout -b master master_copy</font>  �����������
  48. <font color=OrangeRed>git checkout features/performance</font>  ����Ѵ��ڵ�features/performance��֧
  49. <font color=OrangeRed>git checkout --track hotfixes/BJVEP933</font>  ���Զ�̷�֧hotfixes/BJVEP933���������ظ��ٷ�֧
  50. <font color=OrangeRed>git checkout v2.0</font>  ����汾v2.0
  51. <font color=OrangeRed>git checkout -b devel origin/develop</font>  ��Զ�̷�֧develop�����±��ط�֧devel�����
  52. <font color=OrangeRed>git checkout -- README</font>  ���head�汾��README�ļ����������޸Ĵ�����ˣ�
  53. <font color=OrangeRed>git merge origin/master</font>  �ϲ�Զ��master��֧����ǰ��֧
  54. <font color=OrangeRed>git cherry-pick ff44785404a8e</font>  �ϲ��ύff44785404a8e���޸�
  55. <font color=OrangeRed>git push origin master</font>  ����ǰ��֧push��Զ��master��֧
  56. <font color=OrangeRed>git push origin :hotfixes/BJVEP933</font>  ɾ��Զ�ֿ̲��hotfixes/BJVEP933��֧
  57. <font color=OrangeRed>git push --tags</font>  ������tag���͵�Զ�ֿ̲�
  58. <font color=OrangeRed>git fetch</font>  ��ȡ����Զ�̷�֧�������±��ط�֧������merge��
  59. <font color=OrangeRed>git fetch --prune</font>  ��ȡ����ԭ����֧���������������ɾ���ķ�֧
  60. <font color=OrangeRed>git pull origin master</font>  ��ȡԶ�̷�֧master��merge����ǰ��֧
  61. <font color=OrangeRed>git mv README README2</font>  �������ļ�READMEΪREADME2
  62. <font color=OrangeRed>git reset --hard HEAD</font>  ����ǰ�汾����ΪHEAD��ͨ������mergeʧ�ܻ��ˣ�
  63. <font color=OrangeRed>git rebase</font>
  64. <font color=OrangeRed>git branch -d hotfixes/BJVEP933</font>  ɾ����֧hotfixes/BJVEP933������֧�޸��Ѻϲ���������֧��
  65. <font color=OrangeRed>git branch -D hotfixes/BJVEP933</font>  ǿ��ɾ����֧hotfixes/BJVEP933
  66. <font color=OrangeRed>git ls-files</font>  �г�git index�������ļ�
  67. <font color=OrangeRed>git show-branch</font>  ͼʾ��ǰ��֧��ʷ
  68. <font color=OrangeRed>git show-branch --all</font>  ͼʾ���з�֧��ʷ
  69. <font color=OrangeRed>git whatchanged</font>  ��ʾ�ύ��ʷ��Ӧ���ļ��޸�
  70. <font color=OrangeRed>git revert dfb02e6e4f2f7b573337763e5c0013802e392818</font>  �����ύdfb02e6e4f2f7b573337763e5c0013802e392818
  71. <font color=OrangeRed>git ls-tree HEAD</font>  �ڲ������ʾĳ��git����
  72. <font color=OrangeRed>git rev-parse v2.0</font>  �ڲ������ʾĳ��ref���ڵ�SHA1 HASH
  73. <font color=OrangeRed>git reflog</font>  ��ʾ�����ύ�����������ڵ�
  74. <font color=OrangeRed>git show HEAD@{5}</font>
  75. <font color=OrangeRed>git show master@{yesterday}</font>  ��ʾmaster��֧�����״̬
  76. <font color=OrangeRed>git log --pretty=format:'%h %s' --graph</font>  ͼʾ�ύ��־
  77. <font color=OrangeRed>git show HEAD~3</font>
  78. <font color=OrangeRed>git show -s --pretty=raw 2be7fcb476</font>
  79. <font color=OrangeRed>git stash</font>  �ݴ浱ǰ�޸ģ���������ΪHEAD״̬
  80. <font color=OrangeRed>git stash list</font>  �鿴�����ݴ�
  81. <font color=OrangeRed>git stash show -p stash@{0}</font>  �ο���һ���ݴ�
  82. <font color=OrangeRed>git stash apply stash@{0}</font>  Ӧ�õ�һ���ݴ�
  83. <font color=OrangeRed>git grep "delete from"</font>  �ļ��������ı���delete from��
  84. <font color=OrangeRed>git grep -e '#define' --and -e SORT_DIRENT</font>
  85. <font color=OrangeRed>git gc</font>
  86. <font color=OrangeRed>git fsck</font>
  87. <font color=OrangeRed>git archive</font>  ����һ���ɹ�������ѹ����

## ѧϰ����
+ ��ʼ��һ��Git�ֿ�ʱ��ʹ��git init���
+ ����ļ���Git�ֿ��Ϊ������
  1. ʹ������git add [file],ע��ɷ������ʹ�ã���Ӷ���ļ���
  2. ʹ������git commit -m "message",����ύ��
+ ע����vi [file]���༭�ļ�������󰴡�i��������༭״̬������--INSERT--�����༭���esc��������:wq�˳���
+ Ҫ��ʱ���չ�����״̬��ʹ��git status���
+ ���git status�������ļ����޸Ĺ���������git diff�鿴�޸����ݣ�
+ ��Ҫ�鿴�ļ�����ʱ������ʹ������cat [file]
+ ������ʷ�汾
  + HEADָ��İ汾���ǵ�ǰ�汾��Git���������ڰ汾��ʷ֮�䴩��
  + ʹ������git reset --hard commit_id ,���ϸ��汾��HEAD^,���ϸ��汾��HEAD^^,����100���汾��HEAD~100��
  + ����ǰ������ʹ��git log�鿴�ύ��ʷ���Ա�ȷ��Ҫ���˵��ĸ��汾
  + Ҫ�ط�δ������git reflog�鿴������ʷ���Ա�ȷ��Ҫ�ص�δ�����ĸ��汾
+ ���⣺�༭���ļ���ʹ��git add [file]ʱ���֣�warning:LF will be replaced by CRLF the next time Git touches it.
  + ԭ�����ı������У�CR��CarriageReturn����LF��LineFeed����CR/LF�ǲ�ͬ����ϵͳ��ʹ�õĻ��з�
  + Dos��Windowsƽ̨�� ʹ�ûس���CR���ͻ��У�LF�������ַ�������һ�У��س�+����(CR+LF)������\r\n��
  + Mac �� Linuxƽ̨��ֻʹ�û��У�LF��һ���ַ�������һ�У�����\n��
+ ���⣺ΪʲôGit����ļ���Ҫadd��commit����
  + ��Ϊcommit����һ���ύ�ܶ��ļ������Կ��Զ��add��ͬ�ļ���Ȼ��һ���ύ���ֿ�
+ ��⹤������汾�⣨���ݴ�����
  + �����������ڵ���������������Ŀ¼
  + �汾�⣺������һ������Ŀ¼.git��������㹤����������Git�İ汾�⣬Git�İ汾������˺ܶණ������������Ҫ�ľ��ǳ�Ϊstage�����߽�index�����ݴ���������GitΪ�����Զ������ĵ�һ����֧master���Լ�ָ��master��һ��ָ���HEAD
+ ���ļ���ӵ�Git�汾��ʱ
  1. git add ʵ�����ǰ��ļ��޸���ӵ��ݴ���
  2. git commit ʵ�����ǰ��ݴ��������������ύ����ǰ��֧��������ǰ��֧���ύ����
+ �����޸�
  + git checkout --file ���Զ������������޸ģ����ļ��ڹ��������޸�ȫ����������Ϊ���������
    1. �ļ����޸ĺ�û�б��ŵ��ݴ����������޸ľͻص��Ͱ汾��һģһ����״̬
    2. �ļ��Ѿ���ӵ��ݴ������������޸ģ������޸ľͻص���ӵ��ݴ������״̬
  + ʹ������git reset HEAD [file]���԰��ݴ������޸ĳ�������unstage�������·Żع�����
  + �Ѿ��ύ�˲����ʵ��޸ĵ��汾��ʱ����Ҫ���������ύ�����Խ��а汾���ˣ�ǰ����û�����͵�Զ�̿�
+ ɾ���ļ�
  + һ������£���ͨ��ֱ�����ļ��������а�û�õ��ļ�ɾ����������rm����ɾ������ʱ�Ĺ������Ͱ汾��Ͳ�һ����
  + ȷ��Ҫ�Ӱ汾����ɾ���ļ����Ǿ�������git rmɾ��������git commit
  + ��ɾʱ�����ڰ汾���ﻹ�У����԰���ɾ���ļ��ָ������°汾��ʹ������git chechout -- file,(ֻ�ᶪʧ���һ�ε��޸�)
    + git checkout��ʵ���ð汾����İ汾�滻�������İ汾�����۹��������޸Ļ���ɾ���������ԡ�һ����ԭ��
    + ע�⣺����û�б���ӵ��汾��ͱ�ɾ�����ļ������޷��ָ���
+ Զ�ֿ̲�
  + ����GitHub�˻���ע��username,password,email
  + SSH���ܣ�����Git�ֿ��GitHub�ֿ�֮��Ĵ�����ͨ��SSH���ܵ�
    1. ����SSH Key��ssh-keygen -t rsa -C "youremail@example.com" ��һֱ�س���ʹ��Ĭ��ֵ����
    2. ֮��������û���Ŀ¼���ҵ�.sshĿ¼��������id_rsa��id_rsa.pub�����ļ�������������SSH Key����Կ�ԣ�id_rsa��˽Կ������й¶��ȥ��id_rsa.pub�ǹ�Կ�����Ը��߱���
    3. ��¼GitHub->settings->SSH and GPG keys->��дtitle->��key�ı�����ճ��id_rsa.pub����->add key
  + ����һ���ֿ�
    + ��ͷ���ҵ���+��->new repository->��дRepository name->creat repository
  + ����һ��Զ�̿⣬���git remote add origin git@server-name:path/repo-name.git
    + ����һ��Զ�̿�ʱ�����Զ�̿�ָ��һ�����֣�origin��Ĭ��ϰ������
    + ������ʹ������git push -u origin master��һ������master��֧����������
    + �˺󣬱����ύ�󣬿���ʹ������git push origin master���������޸�
  + ɾ��Զ�ֿ̲�
    + ʹ��git remote rm [name]����
    + ʹ��ǰ����������git remote -v�鿴Զ�̿���Ϣ
    + �˴��ġ�ɾ������ʵ�ǽ���˱��غ�Զ�̵İ󶨹�ϵ��������������ɾ����Զ�̿�
  + ��¡Զ�ֿ̲�
    + git clone git@server-name:path/repo-name.git
    + Git֧�ֶ���Э�飬Ĭ�ϵ�git://ʹ��ssh����Ҳ����ʹ��https������Э��
+ ��֧
  + ������֧���л����÷�֧�������֧dev����git checkout -b dev
  + git checkout�������-b������ʾ�������л����൱���������git branch dev��git checkout dev
  + ��git branch����鿴��ǰ��֧��git branch������г����з�֧����ǰ��֧ǰ����һ��*��
  + git merge�������ںϲ�ָ����֧����ǰ��֧
  + �������л����µ�dev��֧��git switch -c dev
  + ֱ���л������е�master��֧��git switch master
+ �����ͻ
  + ����ͬ��֧���Զ����µ��ύʱ��Git�޷����ٺϲ���ֻ����ͼ�����Ե��޸ĺϲ������������ֺϲ����ܻ��г�ͻ
  + git status�����������ǳ�ͻ���ļ�
  + ��cat [file]�鿴�ļ�ʱ��Git��<<<<<<<��=======��>>>>>>>��ǳ���ͬ��֧������
  + ��ͻ������Ҫ�ֶ��޸Ľ����ͻ�󱣴��ύ
  + �����ͻ���ǰ�Git�ϲ�ʧ�ܵ��ļ��ֶ��༭Ϊ����ϣ�������ݣ����ύ
  + ��git log --graph������Կ�����֧�ϲ�ͼ
  + git log --graph --pretty=oneline --abbrev-commit ��֧�ϲ�ͼ�ϼ��
+ ��֧����
  + ͨ���ϲ���֧ʱ��������ܣ�Git����Fast forwardģʽ��������ģʽ�£�ɾ����֧�󣬻ᶪ����֧��Ϣ
  + ���Ҫǿ�ƽ���Fast forwardģʽ��Git�ͻ���mergeʱ����һ���µ�commit���������ӷ�֧��ʷ�ϾͿ��Կ�����֧��Ϣ
  + ������һ����֧devʱ���Ҹ÷�֧�����ύʱ��Ҫʹ����master����֧�Ͻ��кϲ����ҽ���Fast forwardģʽʱ��Ҫע�� --no-ff ����
    + git merge --no-ff -m "..." dev
    + ��Ϊ���κϲ�Ҫ����һ���µ�commit�����Լ���-m��������commit����д��ȥ
+ Bug��֧
  + ��������У�������Ҫ�޸�bug��ÿ��bug�������½���ʱ��֧���޸����޸���ϲ���֧
  + ʹ��git stash������Խ���ǰ������������������֮��ָ����������
  + �޸���bug���л���ԭ����֧���������Ǹɾ��ģ�ֻ����ΪGit��stash���ݴ���ĳ���ط��ˣ���Ҫ�ָ�һ�£��������취��
    1. ��git stash apply�ָ������ǻָ���stash���ݲ���ɾ��������Ҫ��git stash drop��ɾ��
    2. ��git stash pop���ָ���ͬʱ��stash����Ҳɾ��
  + ���Զ��ʹ��stash���ָ���ʱ������git stash list�鿴��Ȼ��ָ�ָ����stash
    + ���git stash apply stash@{0}
  + ���޸���һ����֧�ϵ�bug��������֧��������ͬbugʱ
    + ������git cherry-pick [commit]�����bug�ύ���޸ġ����ơ�����ǰ��֧�������ظ��޸��ļ�
+ Feature��֧
  + ��Ϊ������һ���¹���ʱ�������½�һ��feature��֧�������濪�������ϲ�������֧��ɾ����ʱ��֧
  + ��Ҫ����һ��û�б��ϲ����ķ�֧������ͨ��git branch -D [name]ǿ��ɾ��
+ ����Э��
  + �����½��ķ�֧��������͵�Զ�̣��������˾��ǲ��ɼ���
  + �ӱ������ͷ�֧��ʹ��git push origin branch-name���������ʧ�ܣ�����git pullץȡԶ�̵����ύ
  + �ڱ��ش�����Զ�̷�֧��Ӧ�ķ�֧��ʹ��git checkout -b branch-name origin/branch-name�����غ�Զ�̷�֧���������һ��
  + �������ط�֧��Զ�̷�֧�Ĺ�����ʹ��git branch --set-upstream branch-name origin/branch-name
  + ��Զ��ץȡ��֧��ʹ��git pull������г�ͻ��Ҫ�ȴ����ͻ
+ git rebase�������԰ѱ���δpush�ķֲ��ύ��ʷ�����ֱ��
