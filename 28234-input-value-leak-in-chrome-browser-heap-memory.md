# Input value leak in chrome browser heap memory

> Issue #28234 - Created on 2/5/2024

> Original URL: https://github.com/facebook/react/issues/28234

## Description

Whatever you type in the last focused input, that is getting stored in the chrome browsers heap memory in regex_last_match_info. Even the password is getting stored in plain text. How can I prevent it from storing ? 
