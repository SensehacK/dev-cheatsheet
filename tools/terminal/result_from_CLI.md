# Output


## Save the result from CLI command.

Getting data from Xcode
>  git_tag_result=$(bundle exec fastlane run get_version_number target:"AppName")

Filter the result screen
> git_tag_result=$(echo $git_tag_name | grep "Result:")

Substring
> git_tag_name=${git_tag_result:25}

Access the tag variable in CLI
> swift run xvia tag ${git_tag_name} -p
