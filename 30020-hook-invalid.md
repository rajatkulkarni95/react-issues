# hook invalid

> Issue #30020 - Created on 6/21/2024

> Original URL: https://github.com/facebook/react/issues/30020

## Description

Hi   guys
i have this code, import { Image, ScrollView, Text, View, Alert } from "react-native";
import React, { useState } from "react";
import { SafeAreaView } from "react-native-safe-area-context";
import { StyleSheet } from "react-native";
import { Link } from "expo-router";
import { router } from "expo-router";
import { images } from "../../constants";
import FormField from "../../components/FormField";
import Botao from "../../components/Botao";

function signIn()  {
  const [username, setUsername] = useState('');
const [password, setPassword] = useState('');



  const [isSubmitting, setIsSubmitting] = useState(false);

  //Faz o Sign up
  const submit = async () => {
    if (!username || !password) {
      Alert.alert("Error", "Please fill in all the fields");
    }

    setIsSubmitting(true);

    try {
      await signIn(username, password);
      router.replace("/home");
    } catch (error) {
      Alert.alert("Error", error.message);
    } finally {
      setIsSubmitting(false);
    }
  };

  return (
    <SafeAreaView className="bg-black  h-full">
      <ScrollView>
        <View className="w-full justify-left items-topleft h-full px-6 my-2">
          <Image source={images.logo} className="w-120 h-120" />
          <Text className="text-2xl  text-white">
            Your journey begins now, log in to Onevent today
          </Text>
          <FormField
            style={styles.formField} // Apply consistent styles to all FormField components
            label="Username"
            title="Username"
            placeholder="Write your user"
            value={username}
            onChangeText={(text) => setForm({...username, text })}
            inputmode="username"
          />
          <FormField
            style={styles.formField}
            label="Password"
            title="Password" // Corrected title
            placeholder="Write your password here"
            value={password}
            handleChangeText={(e) => setForm({ ...password, e })}
            otherStyles="mt-6"
            inputmode="password"
          />

          <Botao
            title="Iniciar sessão"
            alignItems="center"
            justifyContent="center"
            containerStyles="w-full mt-7"
            handlePress={submit}
            isLoading={isSubmitting}
          />
          <View className="flex justify-center pt-5 flex-row gap-2">
            <Text className="text-lg text-gray-100 font-pregular">
              Don't have an account?
            </Text>
            <Link
              href="/sign-up"
              className="text-lg font-psemibold text-secondary"
            >
              Signup
            </Link>
          </View>
        </View>
      </ScrollView>
    </SafeAreaView>
  );
};
const styles = StyleSheet.create({
  container: {
    backgroundColor: "white", // Set background color for the entire component
    flex: 1, // Make the container take up the entire viewport height
  },
  content: {
    color: "white",
    padding: 20, // Add padding for better spacing
    alignItems: "center", // Center the content horizontally
  },
  logo: {
    width: 120,
    height: 120,
  },
  heading: {
    fontSize: 24,
    color: "white", // Set text color to white
    marginTop: 20, // Add margin top for spacing
  },
  formField: {
    backgroundColor: "white",
    color: "black", // Set text color to white for all FormField components
    marginTop: 10, // Add margin top between fields
  },
});
export default signIn;
![d5823e0b-e3fe-4061-b657-9e62d309fc2b](https://github.com/facebook/react/assets/65288010/3ecce1d5-d29e-4592-96c2-0fc117a3064b)
butaappears this, anyone know how to solve?
