# Programmatic Navigation

Sometimes we need to take a user to a new page as a result of clicking a button or submitting a page. This is called **programmatic navigation** and is demonstrated below.

**app/users/new/page.tsx:**

```TSX
'use client';
import { useRouter } from 'next/navigation';
import React, { use } from 'react'

const NewUserPage = () => {
    const router = useRouter();

  return (
    <button className='btn btn-primary' onClick={() => router.push('/users')}>Create</button>
  )
}

export default NewUserPage

```