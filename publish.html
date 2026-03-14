<?php
// CORS Headers (Taki HTML app easily data bhej sake)
header("Access-Control-Allow-Origin: *");
header("Access-Control-Allow-Methods: POST");
header("Content-Type: application/json; charset=UTF-8");

// JSON data receive karna
$data = json_decode(file_get_contents("php://input"), true);

if(isset($data['folder_name']) && isset($data['files'])) {
    $folder_name = preg_replace('/[^a-z0-9]/', '', strtolower($data['folder_name'])); // Clean string
    $files = $data['files'];
    
    // Check if folder exists, if not create it
    if (!file_exists($folder_name)) {
        mkdir($folder_name, 0777, true);
    }

    // Saari files folder ke andar save karna
    foreach($files as $filename => $code_content) {
        $safe_filename = basename($filename); // Security
        file_put_contents($folder_name . '/' . $safe_filename, $code_content);
    }

    echo json_encode(["status" => "success", "message" => "Website live ho gayi!"]);
} else {
    echo json_encode(["status" => "error", "message" => "Data incomplete"]);
}
?>
