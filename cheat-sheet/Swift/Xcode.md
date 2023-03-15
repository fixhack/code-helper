## Remove XCUserState

    touch .gitignore

    echo "**/*.xcuserstate"

    git rm --cache *.xcuserstate

    ## Trt this one
    find . -name *.xcuserstate -print0 | xargs -0 git rm --ignore-unmatch