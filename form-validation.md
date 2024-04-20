# Install Packages
``` npm i react-hook-form zod @hookform/resolvers ```
# Create Zod Schema
```Javascript
import { z } from "zod";

export const createSingleAccountSchema = z.object({
  name: z.string().nonempty(),
  email: z.string().email(),
  password: z.string().min(6),
});

// to get the type
// z.infer<typeof createSingleAccountSchema> 
```
# Create The Form 
```Javascript
import { zodResolver } from "@hookform/resolvers/zod";
import React from "react";
import { Controller, useForm } from "react-hook-form";
import { Alert, Text, TextInput, TouchableOpacity, View } from "react-native";
import { createSingleAccountSchema } from "../schema/create-single-account-schema";
import { SafeView } from "./SafeView";
export default function CreateSingleProfile() {
  const { control, handleSubmit } = useForm({
    resolver: zodResolver(createSingleAccountSchema),
    defaultValues: {
      name: "",
      email: "",
      password: "",
    },
  });
  const onSubmit = (data: any) => {
    Alert.alert("Submitted", JSON.stringify(data));
  };
  return (
    <SafeView>
      <View>
        <Text className="text-center py-2 text-blue-500 uppercase">
          Create a new profile
        </Text>
      </View>
      <View>
        <View className="mx-10 py-2">
          <View>
            <Text className=" font-bold py-2">Name</Text>
            <Controller
              control={control}
              name="name"
              render={({
                field: { value, onChange, onBlur },
                fieldState: { error },
              }) => (
                <>
                  <TextInput
                    placeholder="Enter your name"
                    value={value}
                    onChangeText={onChange}
                    onBlur={onBlur}
                    className="p-2 border rounded-md text-black w-full "
                  />
                  {error && (
                    <Text className="text-red-500">{error.message}</Text>
                  )}
                </>
              )}
            />
          </View>
          <View>
            <Text className=" font-bold py-2">Email</Text>
            <Controller
              control={control}
              name="email"
              render={({
                field: { value, onChange, onBlur },
                fieldState: { error },
              }) => (
                <>
                  <TextInput
                    placeholder="Enter your email"
                    value={value}
                    onChangeText={onChange}
                    onBlur={onBlur}
                    className="p-2 border rounded-md text-black w-full "
                  />
                  {error && (
                    <Text className="text-red-500">{error.message}</Text>
                  )}
                </>
              )}
            />
          </View>
          <View>
            <Text className=" font-bold py-2">Password</Text>
            <Controller
              control={control}
              name="password"
              render={({
                field: { value, onChange, onBlur },
                fieldState: { error },
              }) => (
                <>
                  <TextInput
                    placeholder="Enter your password"
                    value={value}
                    onChangeText={onChange}
                    onBlur={onBlur}
                    className="p-2 border rounded-md text-black w-full "
                  />
                  {error && (
                    <Text className="text-red-500">{error.message}</Text>
                  )}
                </>
              )}
            />
          </View>
          <View>
            <TouchableOpacity
              className=" bg-blue-500 my-2 p-2 rounded-md w-full text-center"
              onPress={handleSubmit(onSubmit)}
            >
              <Text className="text-white text-center font-bold">Create</Text>
            </TouchableOpacity>
          </View>
        </View>
      </View>
    </SafeView>
  );
}
```
# Seperate Input Component
```Javascript
import React from 'react'
import { StyleSheet, Text, TextInput } from 'react-native'
import { Controller } from 'react-hook-form';

const MyInput = ({control, name, …otherProps}) => {
  return (
    <Controller
      control={control}
      name={name}
      render={({ field: { value, onChange, onBlur }, fieldState: { error }})=>(
      <>
        <TextInput
        value={value}
        onChangeText={onChange}
        onBlur={onBlur}
        {…otherProps}
        />
        {error && <Text>
                  {error.message}
                  </Text>
        }
      </>
      )}
    />
  )
}
export default MyInput;
```
[reference](https://javascript.plainenglish.io/how-to-build-react-native-forms-with-react-hook-form-and-zod-3fff7d7ee066)
