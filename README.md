# airtable_to_graph

This Python script retrieves data from an Airtable base, identifies relational columns, and builds a knowledge graph using the retrieved data. The knowledge graph is then visualized using the pyvis library and displayed in a web application built with Flask.

It works well with small Airtables but I'm having some issues when the Airtable is too big.

## Prerequisites

Before running the script, ensure that you have the following:

- Python 3.x installed
- Required Python packages: `requests`, `flask`, `pyairtable`, `pyvis`
- Airtable API key (see instructions below)

## Installation

1. Clone the repository:

  ```
  git clone https://github.com/yoheinakajima/airtable_to_graph.git
  ```

2. Navigate to the project directory:

  ```
  cd airtable_to_graph
  ```

3. Install the required Python packages:

  ```
  pip install -r requirements.txt
  ```

## Obtaining Airtable API Key

To retrieve data from Airtable, you need to provide your Airtable API key. Here's how you can find your API key:

1. Log in to your Airtable account.
2. Go to the Developer Hub settings by clicking on your profile picture in the top-right corner and selecting "Developer Hub".
3. In the Personal Key page, click on "Create New Token" button on top right.
4. Give the token a name, and give it the Scopes permissions of data.records:read and schema.bases:read.
5. Add all bases, or select the base you want to connect.
6. Click "Create Token" button and copy the generated API key.

## Configuration

1. Set the following environment variables with your Airtable API key and base ID:

  ```
  export AIRTABLE_API_KEY=your_api_key_here
  ```

  Replace `your_api_key_here` with your actual Airtable API key and `your_base_id_here` with the ID of the Airtable base you want to retrieve data from.

## Usage

1. Run the script:

  ```
  python main.py
  ```

2. Open a web browser and navigate to `http://localhost:5000` to view the knowledge graph.

## How It Works

1. The script retrieves all table names from the specified Airtable base using the Airtable API.
2. It retrieves data from each table using parallel processing with `ThreadPoolExecutor`.
3. The script identifies relational columns in the retrieved data by looking for fields that contain a list of strings starting with "rec".
4. It builds a knowledge graph using the `pyvis` library, representing each record as a node and creating edges based on the relational columns.
5. The knowledge graph is saved as an HTML file in the `static` directory.
6. The script uses Flask to render the knowledge graph in a web application, which can be accessed at `http://localhost:5000`.

## Customization

- You can customize the appearance of the knowledge graph by modifying the `height`, `width`, `bgcolor`, and `font_color` parameters in the `build_knowledge_graph` function.
- If you want to change the shape of the nodes, you can modify the `shape` parameter in the `net.add_node` function.

## Contributing

Contributions are welcome! If you find any issues or have suggestions for improvements, please open an issue or submit a pull request on the GitHub repository.

## License

This project is licensed under the [MIT License](LICENSE).
