1. [Export Automl Edge model](https://cloud.google.com/vertex-ai/docs/export/export-edge-model) as Container format to create saved_model.pb in a gcs bucket using UI/ Vertex SDK
1. Copy the exported container model to your machine: `gsutil cp gs://automl_edge/../saved_model.pb /tmp/automl/001/saveds_model.pb`
1. [Tensorflow Serving with Docker Setup Docker](https://www.tensorflow.org/tfx/serving/docker)
    
    1. Setup [Tensorflow serving](https://www.tensorflow.org/tfx/serving/setup)
    1. Install [Docker](https://www.tensorflow.org/tfx/serving/docker#install_docker)
    1. Pull Serving Image: `docker pull tensorflow/serving`
    1. Run Serving Image: 

        `tensorflow_model_server --port=8500 --rest_api_port=8501 \
        --model_name=automl_edge --model_base_path=/tmp/automl`

1. Send Inference Request:
    
    1. Leverage curl the localhost endpoint or for sample Python request see: `automl_edge/inference_tf_saved_model.py`
        1.  Example Output Run `python automl_edge/inference_tf_saved_model.py` 

            `{'predictions': [{'key': 'test_windshield', 'scores': [0.0226405468, 0.026481336, 0.889754891, 0.0346419364, 0.026481336], 'labels': ['engine_compartment', 'lateral', 'windshield', 'hood', 'bumper']}]}`
