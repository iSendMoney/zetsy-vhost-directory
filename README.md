# zetsy-vhost-directory

### Node.js - Flow to return the store id to clients.
vHost module can be used in Node.js Application to serve the files or redirect. But we only define the store id and return as per the request.
```
1. jcka.zetsy.store =node> jcka(subdomain)
2. jcka =node> ObjectId(123...789)
3. node(ObjectId) =next.js> [store].js
Thus, renders products in server and will return to crawlers. with using 
const getServerSideProps = async ({ req }) => {
  const subdomain = req.headers.host.split('.')[0];
```

### Next.js - Flow for setting subdomains request.
But, ideal solution is to use dynamic routes and the `getServerSideProps` function to serve different content based on the subdomain. 

1. Create a new folder in your Next.js project called pages.
2. Inside the pages folder, create a new folder called [store]. This will create a dynamic route that matches any subdomain.
3. Inside the [store] folder, create a new file called index.js. This file will contain the logic for serving content based on the subdomain.
4. In the index.js file, import the getServerSideProps function:
```
import { getServerSideProps } from 'next';
```
5. Define the getServerSideProps function to get the subdomain from the request:
```
export const getServerSideProps = async ({ req }) => {
  const subdomain = req.headers.host.split('.')[0];

  return {
    props: {
      subdomain,
    },
  };
};
```
```
const Store = ({ subdomain }) => {
  let content;

  if (subdomain === 'store1') {
    content = <p>This is Store 1.</p>;
  } else if (subdomain === 'store2') {
    content = <p>This is Store 2.</p>;
  } else {
    content = <p>This is a default page.</p>;
  }

  return (
    <>
      <h1>{subdomain}</h1>
      {content}
    </>
  );
};

export default Store;
```
![image](https://user-images.githubusercontent.com/102910615/236899434-6457a77a-511c-4b56-b29d-24065b292593.png)
