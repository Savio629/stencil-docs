---
title: How to Create a Molecule
sidebar_label: Create New Molecule
---



<head>
  <title> Create New Molecule </title>
  <meta
    name="description"
    content="your meta content goes here"
  />
</head>

Start by designing a molecule in the [molecule repository](https://github.com/SamagraX-Stencil/ui-templates/tree/dev/src/molecules). When doing so, create a new folder under `/src/molecules`. Consider the different configurations and customizations that could be applied to make the molecule versatile and visually appealing. 
The process of creating a molecule involves several steps.

## Folder Structure

Ensure that the below files/folders are present in the newly created molecule folder:

### Assets

The asset folder within the molecule serves as a centralized location for storing static files and resources that are essential for your molecule. These assets typically include images, fonts, and other static files.

### config.json

This file allows you to customize various aspects of your molecule without directly modifying the source code, making it easier to manage and maintain. The config.json file follows a structured format, typically in JSON (JavaScript Object Notation), where each configuration setting is defined as a key-value pair. Below is an example of the structure:

```
{
  "component": {
    "allowOverride": false,
    "title": "Coming Soon!",
    "description": "We are going to launch this feature very soon. Stay tuned!",
    "backText": "Back"
  }
}
```

### index.tsx

The index.tsx file is used as the entry point for a specific molecule within the application. This file serves as the main file that other parts of the molecule can import to use the functionality provided by the component.

```
import React, { useCallback } from 'react';
import styles from './index.module.css';
import Box from '@mui/material/Box';
import Button from '@mui/material/Button';
import Typography from '@mui/material/Typography';
import {component} from './config.json';
import Hourglass from './hourglass';
import { useColorPalates } from '../../molecules/theme-provider/hooks';

const Component: React.FC = () => {
  const theme = useColorPalates();
  const handleBack = useCallback(()=>{
    // window?.history?.back()
    console.log(component.backText ?? "Back Button")
  },[])

  return (
    <>
      <meta
        name="viewport"
        content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0"></meta>
        <Box className={styles.container}>
          <Box><Typography variant='h4' sx={{color: theme?.primary?.main, fontWeight: "700"}}>{component.title ?? "Coming Soon"}</Typography></Box>
          <Box><Hourglass fillColor={theme?.primary?.main}/></Box>
          <Box><Typography variant='body1' sx={{fontWeight:"600", textAlign: "center"}}>{component.description?? "Coming Soon Description"}</Typography></Box>
          <Box><Button variant='contained' className={styles.backButton} size='large' style={{backgroundColor: theme?.primary?.main}} onClick={handleBack}>{component.backText ?? "Back Button"}</Button></Box>
        </Box>
    </>
  );
};

export default Component;
```

### index.module.css

The index.module.css file is a CSS Module file commonly used to provide scoped styling for component. CSS Modules offer a way to encapsulate styles by generating unique class names for each component, preventing style conflicts and promoting modularity within your molecule.

```
.container{
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  row-gap: 16px;
  font-family: sans-serif !important;
}
```

### index.stories.tsx

The index.stories.tsx file is a `TypeScript` file commonly used in conjunction with Storybook to create and document visual components. Storybook is an open-source tool for developing UI components in isolation, making it easier to build and document user interface elements.

### index.test.tsx

The index.test.tsx file is a TypeScript file used to define and execute unit tests that verify the behavior and functionality of the molecule. These tests ensure that component renders correctly, handle user interactions appropriately, and maintain expected behavior across different scenarios.
Below is an example of how index.test.tsx can be used to write unit tests:

```
import React from 'react';
import { render } from '@testing-library/react';
import Component from './index';

test('renders component with default props', () => {
  // Arrange
  const { getByTestId } = render(<Component />);
  
  // Act
  const componentElement = getByTestId('component');
  
  // Assert
  expect(componentElement).toBeInTheDocument();
});
```
