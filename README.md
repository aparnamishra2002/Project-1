# Project-1
import org.opencv.core.*;
import org.opencv.imgproc.Imgproc;
import org.opencv.objdetect.CascadeClassifier;
import org.opencv.videoio.VideoCapture;

public class FaceRecognition {
    public static void main(String[] args) {
        System.loadLibrary(Core.NATIVE_LIBRARY_NAME);
        
        CascadeClassifier faceDetector = new CascadeClassifier("path/to/haarcascade_frontalface_alt.xml");
        VideoCapture camera = new VideoCapture(0);
        Mat frame = new Mat();

        if (camera.isOpened()) {
            while (true) {
                camera.read(frame);
                MatOfRect faceDetections = new MatOfRect();
                faceDetector.detectMultiScale(frame, faceDetections);

                for (Rect rect : faceDetections.toArray()) {
                    Imgproc.rectangle(frame, new Point(rect.x, rect.y), 
                                     new Point(rect.x + rect.width, rect.y + rect.height), 
                                     new Scalar(0, 255, 0));
                }
                // Display the frame with detected faces
                // Add GUI logic here to show the frame
            }
        }
        camera.release();
    }
}
