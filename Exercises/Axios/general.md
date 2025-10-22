# Axios Exercises with React

## Exercise 1: Simple GET Request

### Objective

Make a simple GET request to fetch data from an API.

### Solution

#### Install Axios

```bash
npm install axios
```

#### Create a Component

```jsx
import React, { useEffect, useState } from "react";
import axios from "axios";

const SimpleGet = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/posts/1")
      .then((response) => {
        setData(response.data);
      })
      .catch((error) => {
        console.error("There was an error!", error);
      });
  }, []);

  return (
    <div>
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : "Loading..."}
    </div>
  );
};

export default SimpleGet;
```

## Exercise 2: Handling POST Request

### Objective

Make a POST request to send data to an API.

### Solution

#### Create a Component

```jsx
import React, { useState } from "react";
import axios from "axios";

const PostRequest = () => {
  const [data, setData] = useState(null);

  const handleSubmit = () => {
    axios
      .post("https://jsonplaceholder.typicode.com/posts", {
        title: "foo",
        body: "bar",
        userId: 1,
      })
      .then((response) => {
        setData(response.data);
      })
      .catch((error) => {
        console.error("There was an error!", error);
      });
  };

  return (
    <div>
      <button onClick={handleSubmit}>Submit Data</button>
      {data && <pre>{JSON.stringify(data, null, 2)}</pre>}
    </div>
  );
};

export default PostRequest;
```

## Exercise 3: GET Request with URL Parameters

### Objective

Make a GET request with URL parameters.

### Solution

#### Create a Component

```jsx
import React, { useEffect, useState } from "react";
import axios from "axios";

const GetWithParams = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/posts", {
        params: { userId: 1 },
      })
      .then((response) => {
        setData(response.data);
      })
      .catch((error) => {
        console.error("There was an error!", error);
      });
  }, []);

  return (
    <div>
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : "Loading..."}
    </div>
  );
};

export default GetWithParams;
```

## Exercise 4: Handling PUT Request

### Objective

Make a PUT request to update existing data.

### Solution

#### Create a Component

```jsx
import React, { useState } from "react";
import axios from "axios";

const PutRequest = () => {
  const [data, setData] = useState(null);

  const handleUpdate = () => {
    axios
      .put("https://jsonplaceholder.typicode.com/posts/1", {
        id: 1,
        title: "foo",
        body: "bar",
        userId: 1,
      })
      .then((response) => {
        setData(response.data);
      })
      .catch((error) => {
        console.error("There was an error!", error);
      });
  };

  return (
    <div>
      <button onClick={handleUpdate}>Update Data</button>
      {data && <pre>{JSON.stringify(data, null, 2)}</pre>}
    </div>
  );
};

export default PutRequest;
```

## Exercise 5: Handling DELETE Request

### Objective

Make a DELETE request to remove data.

### Solution

#### Create a Component

```jsx
import React, { useState } from "react";
import axios from "axios";

const DeleteRequest = () => {
  const [status, setStatus] = useState(null);

  const handleDelete = () => {
    axios
      .delete("https://jsonplaceholder.typicode.com/posts/1")
      .then((response) => {
        setStatus("Delete successful");
      })
      .catch((error) => {
        console.error("There was an error!", error);
        setStatus("Delete failed");
      });
  };

  return (
    <div>
      <button onClick={handleDelete}>Delete Data</button>
      {status && <p>{status}</p>}
    </div>
  );
};

export default DeleteRequest;
```

## Exercise 6: Axios Interceptors for Logging

### Objective

Use Axios interceptors to log requests and responses.

### Solution

#### Setup Interceptors

```jsx
import axios from "axios";

axios.interceptors.request.use((request) => {
  console.log("Starting Request", request);
  return request;
});

axios.interceptors.response.use((response) => {
  console.log("Response:", response);
  return response;
});
```

#### Create a Component

```jsx
import React, { useEffect, useState } from "react";
import axios from "axios";

const InterceptorDemo = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/posts/1")
      .then((response) => {
        setData(response.data);
      })
      .catch((error) => {
        console.error("There was an error!", error);
      });
  }, []);

  return (
    <div>
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : "Loading..."}
    </div>
  );
};

export default InterceptorDemo;
```

## Exercise 7: Handling Error Responses

### Objective

Properly handle error responses from an API.

### Solution

#### Create a Component

```jsx
import React, { useEffect, useState } from "react";
import axios from "axios";

const ErrorHandling = () => {
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);

  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/invalid-endpoint")
      .then((response) => {
        setData(response.data);
      })
      .catch((error) => {
        setError(error.response ? error.response.data : "Network Error");
      });
  }, []);

  return (
    <div>
      {error ? (
        <p>Error: {error}</p>
      ) : (
        <pre>{JSON.stringify(data, null, 2)}</pre>
      )}
    </div>
  );
};

export default ErrorHandling;
```

## Exercise 8: Canceling Requests

### Objective

Implement request cancellation to avoid memory leaks and unnecessary network calls.

### Solution

#### Create a Component

```jsx
import React, { useEffect, useState } from "react";
import axios from "axios";

const CancelRequest = () => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const source = axios.CancelToken.source();

    axios
      .get("https://jsonplaceholder.typicode.com/posts/1", {
        cancelToken: source.token,
      })
      .then((response) => {
        setData(response.data);
        setLoading(false);
      })
      .catch((error) => {
        if (axios.isCancel(error)) {
          console.log("Request canceled", error.message);
        } else {
          console.error("There was an error!", error);
        }
        setLoading(false);
      });

    return () => {
      source.cancel("Component unmounted");
    };
  }, []);

  return (
    <div>
      {loading ? "Loading..." : <pre>{JSON.stringify(data, null, 2)}</pre>}
    </div>
  );
};

export default CancelRequest;
```

## Exercise 9: Axios Instance for Custom Configurations

### Objective

Create and use an Axios instance with custom configurations.

### Solution

#### Setup Axios Instance

```jsx
import axios from "axios";

const axiosInstance = axios.create({
  baseURL: "https://jsonplaceholder.typicode.com",
  timeout: 1000,
  headers: { "X-Custom-Header": "foobar" },
});

export default axiosInstance;
```

#### Create a Component

```jsx
import React, { useEffect, useState } from "react";
import axiosInstance from "./axiosInstance";

const CustomAxiosInstance = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    axiosInstance
      .get("/posts/1")
      .then((response) => {
        setData(response.data);
      })
      .catch((error) => {
        console.error("There was an error!", error);
      });
  }, []);

  return (
    <div>
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : "Loading..."}
    </div>
  );
};

export default CustomAxiosInstance;
```

## Exercise 10: Sequential Requests

### Objective

Handle multiple requests in sequence.

### Solution

#### Create a Component

```jsx
import React, { useEffect, useState } from 'react';
import axios from 'axios';

const SequentialRequests = () => {
  const [firstPost, setFirstPost] = useState(null);
  const [secondPost, setSecondPost] = useState(null);

  useEffect(() => {
    axios.get('https://jsonplaceholder.typicode.com/posts/1')
      .then(response => {
        setFirstPost(response.data);
        return axios.get('https://jsonplaceholder.typicode.com/posts

/2');
      })
      .then(response => {
        setSecondPost(response.data);
      })
      .catch(error => {
        console.error('There was an error!', error);
      });
  }, []);

  return (
    <div>
      <h2>First Post</h2>
      {firstPost ? <pre>{JSON.stringify(firstPost, null, 2)}</pre> : 'Loading...'}
      <h2>Second Post</h2>
      {secondPost ? <pre>{JSON.stringify(secondPost, null, 2)}</pre> : 'Loading...'}
    </div>
  );
};

export default SequentialRequests;
```

## Exercise 11: Parallel Requests

### Objective

Handle multiple requests in parallel.

### Solution

#### Create a Component

```jsx
import React, { useEffect, useState } from "react";
import axios from "axios";

const ParallelRequests = () => {
  const [posts, setPosts] = useState([]);
  const [users, setUsers] = useState([]);

  useEffect(() => {
    axios
      .all([
        axios.get("https://jsonplaceholder.typicode.com/posts"),
        axios.get("https://jsonplaceholder.typicode.com/users"),
      ])
      .then(
        axios.spread((postsResponse, usersResponse) => {
          setPosts(postsResponse.data);
          setUsers(usersResponse.data);
        })
      )
      .catch((error) => {
        console.error("There was an error!", error);
      });
  }, []);

  return (
    <div>
      <h2>Posts</h2>
      {posts.length > 0 ? (
        <pre>{JSON.stringify(posts, null, 2)}</pre>
      ) : (
        "Loading..."
      )}
      <h2>Users</h2>
      {users.length > 0 ? (
        <pre>{JSON.stringify(users, null, 2)}</pre>
      ) : (
        "Loading..."
      )}
    </div>
  );
};

export default ParallelRequests;
```

## Exercise 12: Axios with React Hook Form

### Objective

Integrate Axios with React Hook Form for form submissions.

### Solution

#### Install React Hook Form

```bash
npm install react-hook-form
```

#### Create a Component

```jsx
import React from "react";
import { useForm } from "react-hook-form";
import axios from "axios";

const FormWithAxios = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();

  const onSubmit = (data) => {
    axios
      .post("https://jsonplaceholder.typicode.com/posts", data)
      .then((response) => {
        console.log(response.data);
      })
      .catch((error) => {
        console.error("There was an error!", error);
      });
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <label>Title</label>
      <input {...register("title", { required: true })} />
      {errors.title && <span>This field is required</span>}

      <label>Body</label>
      <input {...register("body", { required: true })} />
      {errors.body && <span>This field is required</span>}

      <button type="submit">Submit</button>
    </form>
  );
};

export default FormWithAxios;
```

## Exercise 13: Handling Authentication Tokens

### Objective

Attach authentication tokens to requests.

### Solution

#### Setup Axios Interceptor

```jsx
import axios from "axios";

axios.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem("token");
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);
```

#### Create a Component

```jsx
import React, { useEffect, useState } from "react";
import axios from "axios";

const AuthenticatedRequest = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/posts")
      .then((response) => {
        setData(response.data);
      })
      .catch((error) => {
        console.error("There was an error!", error);
      });
  }, []);

  return (
    <div>
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : "Loading..."}
    </div>
  );
};

export default AuthenticatedRequest;
```

## Exercise 14: File Upload with Axios

### Objective

Handle file uploads using Axios.

### Solution

#### Create a Component

```jsx
import React, { useState } from "react";
import axios from "axios";

const FileUpload = () => {
  const [file, setFile] = useState(null);

  const handleFileChange = (event) => {
    setFile(event.target.files[0]);
  };

  const handleFileUpload = () => {
    const formData = new FormData();
    formData.append("file", file);

    axios
      .post("https://jsonplaceholder.typicode.com/posts", formData, {
        headers: {
          "Content-Type": "multipart/form-data",
        },
      })
      .then((response) => {
        console.log(response.data);
      })
      .catch((error) => {
        console.error("There was an error!", error);
      });
  };

  return (
    <div>
      <input type="file" onChange={handleFileChange} />
      <button onClick={handleFileUpload}>Upload File</button>
    </div>
  );
};

export default FileUpload;
```

## Exercise 15: Implementing a Retry Mechanism

### Objective

Implement a retry mechanism for failed requests.

### Solution

#### Setup Axios Retry

```jsx
import axios from "axios";
import axiosRetry from "axios-retry";

axiosRetry(axios, { retries: 3, retryDelay: axiosRetry.exponentialDelay });
```

#### Create a Component

```jsx
import React, { useEffect, useState } from "react";
import axios from "axios";

const RetryRequest = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/posts/1")
      .then((response) => {
        setData(response.data);
      })
      .catch((error) => {
        console.error("There was an error!", error);
      });
  }, []);

  return (
    <div>
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : "Loading..."}
    </div>
  );
};

export default RetryRequest;
```

```

```
