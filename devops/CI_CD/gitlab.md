## 异常处理
1. projectxxx/settings/integrations.500 error.
原因是由于webhook配置错误(url无法正常解析),通过删除webhook解决问题

```
# 1. 进入shell命令行
gitlab-rails console

# 2. 通过gitlab shell查找webhooks,id对应项目主页面的项目id,例如(31)
project = Project.find_by_full_path(31)
# 3. 输出所有的hooks,并获取,例如: ProjectHook id: 10
project.hooks.map()
# 4. 在linux shell中 通过gitlab api删除

curl --header "Private-Token: xxx" -X DELETE "https://gitlab.myinstance.com/api/v4/projects/31/hooks/10"


```
* 参考: https://gitlab.com/gitlab-org/gitlab-foss/-/issues/53465