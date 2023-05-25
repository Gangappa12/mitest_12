Spring Example
java
This minimal example shows how to use JavaFX (FXML) with the glorious Spring Framework (and Maven). Both frameworks have an entry point, which is Application.launch(...) for JavaFX and SpringApplication.run(...) for Spring. By creating the simple helper-class SpringFXMLLoaderFactory, we solve this problem.

Showing The Primary Stage
The first time opening a stage (with the primaryStage), call the SpringFXMLLoaderFactory.getLoader(...) method. You should pass some arguments. They can be retrieved by super.getParameters().getRaw().toArray(new String[0]) in your class extending javafx.application.Application. No need to set the ControllerFactory of the loader - the SpringFXMLLoaderFactory will already have done that for you, with a reference to the getBean(...) method of the just created application context.

Example:

FXMLLoader loader = SpringFXMLLoaderFactory.getLoader(this.getClass().getClassLoader().getResource("main.fxml"), super.getParameters().getRaw().toArray(new String[0]));
Parent root = loader.load();
Scene scene = new Scene(root, -1, -1, false, SceneAntialiasing.BALANCED);
primaryStage.setTitle("Main Stage");
primaryStage.setScene(scene);
primaryStage.show();
done
