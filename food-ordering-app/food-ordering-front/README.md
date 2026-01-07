# 🍕 Food Ordering Frontend - React

Frontend application for Food-Ordering-Delivery-Web-Application built with React 18 and Redux.

## Overview

This is the client-side application for the food ordering system. It provides a fully responsive interface for users to:
- Browse restaurant menu
- Place orders
- Track deliveries
- Manage user accounts
- Admin order management
- Employee delivery tracking

## Tech Stack

- **React 18** - UI library with React Hooks
- **Redux & Redux-Persist** - State management
- **React Router v6** - Client-side routing
- **Axios** - HTTP client
- **Bootstrap 5** - UI framework
- **Styled Components** - CSS-in-JS styling
- **SweetAlert2** - User notifications

## Quick Start

### Prerequisites
- Node.js v14+
- npm or yarn

### Installation

```bash
# Install dependencies
npm install

# Start development server
npm start

# Open browser to http://localhost:3000
```

### Build for Production

```bash
npm run build
```

## Available Scripts

### `npm start`
Runs the app in development mode at [http://localhost:3000](http://localhost:3000)

### `npm test`
Launches the test runner in interactive watch mode

### `npm run build`
Builds the app for production to the `build` folder

### `npm run eject`
**Note:** This is a one-way operation. Not reversible.

## Project Structure

```
src/
├── components/          # React components
├── services/            # API communication
├── store-redux/         # Redux store
├── images/             # Images and assets
├── App.js              # Main app component
└── index.js            # Entry point
```

## Available Components

- **Navigation:** NavbarComponent, FooterComponent
- **Authentication:** LoginComponent, RegistrationComponent
- **Menu:** MenuMealTypeComponent, ListMealByMealTypeComponent
- **Cart:** CartComponent, EditItemQuantityComponent
- **Orders:** CartComponent, FinalOrderByIdComponent
- **User:** MyProfileComponent, MyActiveFinalOrdersComponent
- **Admin:** ListMealComponent, ListMealTypeComponent, ListUserComponent
- **Employee:** ActiveFinalOrdersComponent, OrderHistoryComponent

## API Integration

Services for API communication:
- `LoginService` - Authentication
- `MealService` - Meal management
- `MealTypeService` - Category management
- `UserService` - User management
- `TokenService` - Token handling

## State Management

Redux store for:
- Cart state
- Authentication
- User data
- Global UI state

## Environment Variables

Create `.env` file in the root:

```
REACT_APP_API_URL=http://localhost:8080
REACT_APP_API_VERSION=v1
```

## Styling

- Bootstrap 5 for layout and components
- Custom CSS files for component-specific styling
- Styled Components for dynamic styling

## Authentication

- JWT token-based authentication
- Automatic token injection in requests
- Token refresh handling
- Role-based access control

## Responsive Design

- Mobile-first approach
- Breakpoints for tablet and desktop
- Flexible layouts with Bootstrap Grid

## Performance Optimization

- Code splitting with React.lazy()
- Image optimization
- Redux selectors for memoization
- CSS minification in production build

## Testing

```bash
npm test
```

## Build & Deployment

### Development
```bash
npm start
```

### Production Build
```bash
npm run build
```

### Deployment
The `build` folder is ready to be deployed on any static hosting service.

## Troubleshooting

### Port 3000 Already in Use
```bash
set PORT=3001
npm start
```

### Can't Connect to Backend
- Verify backend is running on port 8080
- Check CORS configuration
- Clear browser cache

### Dependencies Issues
```bash
rm -r node_modules
npm install
npm start
```

## Learn More

- [React Documentation](https://react.dev/)
- [Redux Documentation](https://redux.js.org/)
- [React Router Documentation](https://reactrouter.com/)
- [Bootstrap Documentation](https://getbootstrap.com/)

## Developer

**Nidhi Kumari**
- 📧 Email: nidhikumari934181@gmail.com
- 💼 LinkedIn: linkedin.com/in/nidhi-kumari-4648692b2
- 💻 GitHub: github.com/nidhikumari30

## License

This project is open source under the MIT License.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
