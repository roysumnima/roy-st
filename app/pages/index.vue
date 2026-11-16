
<template>
  <UContainer style="min-height: 100vh; position: relative; display: flex; flex-direction: column; align-items: center; padding-top: 2rem; padding-bottom: 2rem;">
    <h1 style="font-size: 2rem; position: absolute; top: 20%; left: 0; width: 100%; text-align: center;"> ⭐️ welcome to <span style="background: darkslategray; color: white;">roy st </span> ⭐️</h1>

    <div style="position: absolute; top: 40%; left: 0; width: 100%; display: flex; justify-content: center;">
      <div id="house-links" style="display: flex; gap: 1rem; justify-content: center; align-items: center;">
        <HouseLink to="https://roysumnima.github.io/">🏠</HouseLink>
        <HouseLink to="https://www.instagram.com/justrghost/">🏠</HouseLink>
        <HouseLink to="https://ko-fi.com/justrghost">🏠</HouseLink>
      </div>
    </div>

    <div style="margin-top: auto;">
      <Bike />
    </div>
  </UContainer>
</template>
