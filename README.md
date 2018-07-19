这是个操作githubzpi的说明
操作github上的库用的是githubapiv3
使用pyhton requests完成
	requests的 get post patch put delete 的几种方法实现主要使用到了get post
代码实现
相关资源地址：https://developer.github.com/v3/pulls/#get-if-a-pull-request-has-been-merged
# 获取pullRequest的相关信息
GET /repos/:owner/:repo/pulls
Parameters
Name	Type	Description
state	string	Either open, closed, or all to filter by state. Default: open
head	string	Filter pulls by head user and branch name in the format of user:ref-name. Example: github:new-script-format.
base	string	Filter pulls by base branch name. Example: gh-pages.
sort	string	What to sort results by. Can be either created, updated, popularity (comment count) or long-running (age, filtering by pulls updated in the last month). Default: created
direction	string	The direction of the sort. Can be either asc or desc. Default: desc when sort is created or sort is not specified, otherwise asc.

for exemper:
url="api.github.com/repos/jainlaipinan/acrn/pulls"
requests.get(url)

# rebase and merge 相关操作
Merge a pull request (Merge Button)
Input
Name	Type	Description
commit_title	string	Title for the automatic commit message.
commit_message	string	Extra detail to append to automatic commit message.
sha	string	SHA that pull request head must match to allow merge.
merge_method	string	Merge method to use. Possible values are merge, squash or rebase. Default is merge.
Response if merge was successful
Status: 200 OK
{
  "sha": "6dcb09b5b57875f334f61aebed695e2e4193db5e",
  "merged": true,
  "message": "Pull Request successfully merged"
}

