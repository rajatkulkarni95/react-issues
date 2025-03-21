# Feature: useEffectEvent should be useCallback without dependency array

> Issue #27793 - Created on 12/5/2023

> Original URL: https://github.com/facebook/react/issues/27793

## Description

The experimental useEffectEvent is generally something useCallback should have been without depedency array or with empty dependency array to match the behavior of useEffect. Introducing new name will just bring more confusion since it's very hard to image, what useEffectEvent should do...🙏🏻✌🏻👀
