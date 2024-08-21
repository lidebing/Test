## git commit msg检查
```shell
#!/bin/sh

# 启用大小写不敏感
shopt -s nocasematch


 # echo "Script name: $0"
 # echo "Number of arguments: $#"
 # echo "All arguments: $*"

 # 处理每个参数
 # for arg in "$@"; do
 #     echo "Argument: $arg \n"
 # done

# message（用户手动输入的提交信息）、template（使用了提交信息模板）或者 merge（自动合并时生成的提交信息）
git_command_type=$1

# TODO 不需要检查.git/MERGE_MSG(merge的)、.git/COMMIT_EDITMSG(commit)，这个地方需要注意prepare-commit-msg和commit-msg获取到的参数列表是不一样的
skipCheckMsg=(".git/MERGE_MSG")

# 判断输入是否在数组中
if [[ " ${skipCheckMsg[@]} " =~ " $git_command_type " ]]; then
    exit 0
fi


commit_msg_file=$1
commit_msg=$(cat $1)
commit_msg=$(echo "$commit_msg" | tr '[:upper:]' '[:lower:]')

types="Bugfix|Feature|Improve|Refactor|Doc|CI|Test"

validCommitMsg=true
patternType="^\[($types)\]"
# 检查输入值是否符合规范
if [[ $commit_msg =~ $patternType ]]; then
    :
else
    echo "Type不规范, 使用[$types]"
    validCommitMsg=false
fi

# 验证ticket number
patternTicket="\[EXTMSEN-[0-9]+\]"
# 检查输入值是否符合规范
if [[ $commit_msg =~ $patternTicket ]]; then
    :
else
    echo "Ticket不规范, 使用[EXTMSEN-number]"
    validCommitMsg=false
fi

patternDesc=".*\[(.*)\][^[]*$"
# 使用正则表达式匹配最后一个方括号中的内容
if [[ $commit_msg =~ $patternDesc ]]; then
    content_inside_brackets=${BASH_REMATCH[1]}
    if [ -n "$content_inside_brackets" ]; then
        :
    else
        echo "Desc不规范, 不能为空"
        validCommitMsg=false
    fi
else
    echo "Desc不规范, Desc放在[]中. 格式为[type][EXTMSEN-number][Desc不能为空]"
    validCommitMsg=false
fi

# echo "检查结果: $validCommitMsg"
if [ "$validCommitMsg" = false ]; then
    echo "当前信息：${commit_msg}"
    echo "标准格式：[type][EXTMSEN-number][Desc不能为空]"
    exit 1
fi
```

## 其他工具
