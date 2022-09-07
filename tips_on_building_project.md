## Tips on building the data flywheel

------

- Scope the product
- Build the skeleton of the ML-powered product
  - Start with a subset of the data set
  - Build a baseline model or even a dummy classifier
  - Build a user interface quickly e.g. in Streamlit
  - Make an API e.g. in FastAPI
  - Deploy and make the system available to target users such they can interact with the product
- Make sure that everything works end-to-end. Do not worry, there will be a lot of challenges along the way:
  - How will users interact with the product?
  - What is the user input and what is the output?
  - How do users signup and sign in to the system?
  - How do we gather feedback from users?
  - How do we measure churn rate?
- When the end-to-end pipeline works:
  - Build a model that already works in the text domain e.g. sentiment classification
- Then work on making the current ML-powered product better

## Tips on team work


------

- Divide the work into main responsibilities or roles so people can work independently, for example:
  - Data: gathering data, pre-processing, feature engineering, and make the data ready for modelling
  - ML: training and evaluation of models, both dummy classifiers, baselines and also advanced models
  - Operations: take trained models and deployed them as API servers. Also responsible for building the UI and monitoring
- Determine and make expectations clear between the team members
- Working in the same time zone helps a lot
- Schedule weekly or bi-weekly syncs in addition to Discord chats
  - Send out calendar invitations
- Set up tools for organizing tasks e.g. Notion

## Tips on project demo

------

- Think of the demonstration as a pitch for potential investors
- Focus on the wow effect during the project demo
- Have a good story to tell behind why the product is needed
- Make a beautiful UI
- Record a video e.g. in Loom