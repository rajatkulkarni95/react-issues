# Bug: Expected Static Flag was missing. Please Notify React Team

> Issue #31690 - Created on 12/6/2024

> Original URL: https://github.com/facebook/react/issues/31690

## Description

React version:
    "react": "18.3.1",

## Steps To Reproduce

```
const MessagesDetailsPage = () => {
  const { id, orderId } = useLocalSearchParams<{
    id: string;
    orderId?: string;
  }>();
  const {
    mutateAsync: sendMessage,
    isPending: isSending,
    variables,
  } = useSendMessage();
  const { data, isPending, hasNextPage, fetchNextPage, isFetchingNextPage } =
    useGetUserMessagesById(Number(id));

  if (isPending)
    return (
      <View className="flex-1 bg-background justify-center items-center">
        <ActivityIndicator size={"large"} />
        <Stack.Screen
          options={{
            headerShown: screenHeaderShown,
            title: "Loading...",
            headerBackTitle: "back",
          }}
        />
      </View>
    );

  const messages = data?.pages?.flatMap((item) => item?.content) || [];
  const user = data?.pages[0]?.user;
  const canReply = data?.pages[0]?.canReply;
  const loadMore = () => {
    if (hasNextPage && !isFetchingNextPage) {
      fetchNextPage();
    }
  };
  return (
    <View className={cn("flex-1 bg-background", !!orderId ? "pb-14" : "")}>
      <Stack.Screen
        options={{
          title: user?.name,
          headerBackTitle: "back",
        }}
      />
      <KeyboardAvoidingView
        className="flex-1 bg-background p-3"
        keyboardVerticalOffset={isIOS ? 80 : 0}
        behavior={isIOS ? "padding" : "height"}
      >
        <ChatArea
          isFetchingNextPage={isFetchingNextPage}
          messages={messages}
          onLoadMore={loadMore}
          isSending={isSending}
          variables={variables}
        />
        {canReply ? (
          <MessageActions sendMessage={sendMessage} isPending={isSending} />
        ) : (
          <View className="items-center p-2">
            <P>You can't reply to this user</P>
          </View>
        )}
      </KeyboardAvoidingView>
    </View>
  );
};

export default MessagesDetailsPage;
```

```
import { MessagesSquare } from "@/components/icons/message-square-icon";
import { P } from "@/components/ui/typography";
import useI18n from "@/hooks/useI81n";
import { IChatMessage, IMessageInput } from "@/types/IChat";
import { FlashList } from "@shopify/flash-list";
import React, { useRef } from "react";
import { ActivityIndicator, View } from "react-native";
import { ChatMessages } from "../chat-messages";
import { MessagePendingStates } from "../message-pending-states";

export type ChatAreaProps = {
  messages: IChatMessage[];
  className?: string;
  isFetchingNextPage: boolean;
  onLoadMore: () => void;
  footerComponent?: React.ReactNode;
  isSending?: boolean;
  variables?: IMessageInput;
  hasNextPage?: boolean;
};

export const ChatArea = ({
  messages,
  className,
  isFetchingNextPage,
  onLoadMore,
  footerComponent,
  isSending,
  variables,
}: ChatAreaProps) => {
  const { getText } = useI18n();
  const ref = useRef<FlashList<IChatMessage>>(null);
  const thumbnails =
    messages
      ?.map((c) => !!c.image && c.image)
      .filter(
        (url): url is string => typeof url === "string" && url.trim().length > 0
      ) || [];

  const scrollToTop = () => {
    if (ref.current) {
      ref.current.scrollToOffset({
        animated: true,
        offset: 0,
      });
    }
  };

  // useEffect(() => {
  //   scrollToTop();
  // }, [variables]);

  // useEffect(() => {
  //   scrollToTop();
  // }, []);

  return (
    <FlashList
      ref={ref}
      keyboardDismissMode="on-drag"
      keyboardShouldPersistTaps="handled"
      data={messages}
      showsVerticalScrollIndicator={false}
      className={className}
      renderItem={({ item }) => (
        <ChatMessages item={item} thumbnails={thumbnails} />
      )}
      keyExtractor={({ id }) => id.toString()}
      inverted
      estimatedItemSize={100}
      onEndReachedThreshold={0.1}
      ListEmptyComponent={() => (
        <View className="flex-1 bg-background items-center justify-center gap-2">
          <MessagesSquare className="text-foreground" size={40} />
          <P>{getText("send_message")}</P>
        </View>
      )}
      onEndReached={onLoadMore}
      ListHeaderComponent={() => {
        if (isSending) return <MessagePendingStates variables={variables} />;
      }}
      ListFooterComponent={() => {
        return (
          <View>
            {isFetchingNextPage && (
              <View className="py-5 self-center">
                <ActivityIndicator size={"small"} />
              </View>
            )}

            {footerComponent}
          </View>
        );
      }}
    />
  );
};
```

## The current behavior


## The expected behavior

