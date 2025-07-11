1. nextjs에서 mongodb를 사용하기 위해서는 mongoose를 사용한다.
` npm i mongoose `

2. mongodb connect를 위한 펑션 생성
```
mongoose.connect(process.env.MONGODB_URI,
                 { dbName: "your-db-name" });
비동기로 실행되므로 async - await을 사용해야 한다.
```

3. 데이터 모델 생성
```
	const userSchema = new mongoose.Schema(
		{
		    col1: {
		      type: String,
		      required: true,
		      unique: true,
		    },
		    col2: {
		      type: String,
		      required: true,
		    },
		},
		{
		    timestamps: true,
		}
	)
```

4. mongodb data manipulation function 생성
```
export const createOrUpdateUser = async (
  id,
  first_name,
  last_name,
  image_url,
  email_addresses,
  username
) => {
  try {
    await connect();
    const user = await User.findOneAndUpdate(
      { clerkId: id },
      {
        $set: {
          firstName: first_name,
          lastName: last_name,
          avatar: image_url,
          email: email_addresses[0].email,
          username: username,
        },
      },
      { new: true, upsert: true }
    );
    return user;
  } catch (error) {
    console.error("Error creating or updating user:", error);
    throw new Error("Failed to create or update user");
  }
};
```

5.  데이터 조작 실행
```
try {
      await createOrUpdateUser(
        id,
        first_name,
        last_name,
        image_url,
        email_addresses,
        username
      );
      return new Response("User created or updated successfully", {
        status: 200,
      });
    } catch (error) {
      console.error("Error creating or updating user:", error);
      return new Response("Failed to create or update user", { status: 500 });
    }
```

## * 정리
### module install - connection - schema(model) - manipulation function - call function